# Kiến Trúc & Thiết Kế (Design)

← [Về trang chủ](README.md)

## 1. Tổng quan kiến trúc

Hệ thống được xây dựng hoàn toàn trên **Microsoft Power Platform / Dataverse**, theo mô hình pro-code:

```mermaid
flowchart TB
    subgraph UI["Lớp giao diện"]
        GX["10 trang GenUX (React 17 + TypeScript + Fluent UI v9)"]
    end
    subgraph API["Lớp API"]
        CA["6 Dataverse Custom API (bound/unbound)"]
    end
    subgraph LOGIC["Lớp nghiệp vụ (transaction thật)"]
        PL["6 Dataverse Plugin (C#, .NET)"]
    end
    subgraph DATA["Lớp dữ liệu"]
        DV["Dataverse: 20 bảng jas_* + contact"]
    end
    GX -->|"Xrm.WebApi.execute()"| CA
    CA --> PL
    PL -->|"transaction ghi sổ atomic"| DV
    GX -->|"đọc/ghi trực tiếp qua dataApi (CRUD thường)"| DV
```

- **Model-driven app**: "JoiArt Studio Pro" — 1 app duy nhất, 2 khu vực điều hướng (Area): **Main** và **Admin Center**.
- **10 trang GenUX** — không dùng form/view chuẩn (native) ở bất kỳ đâu; toàn bộ giao diện là React tùy biến.
- **6 Custom API + 6 Plugin C#** cho các nghiệp vụ ghi sổ cần transaction thật (atomicity — nếu lỗi giữa chừng, toàn bộ thao tác được rollback).
- Các thao tác CRUD đơn giản (tạo/sửa học viên, danh mục...) đi thẳng qua Dataverse Web API từ trang GenUX, không qua plugin.

## 2. Mô hình dữ liệu

### 2.1. Danh mục các bảng (`jas_*` + `contact`)

| Nhóm | Bảng | Vai trò |
|---|---|---|
| Master data | `jas_class_type` | Loại lớp học |
| | `jas_course_package` | Gói học (giá, số buổi, thời hạn) |
| | `jas_shift` | Ca học |
| | `jas_item` | Họa cụ (có cache tồn kho + giá vốn) |
| | `jas_teacher` | Giáo viên |
| | `jas_app_setting` | Cấu hình chung (singleton — đúng 1 dòng) |
| Học viên | `contact` | Tái sử dụng bảng Contact chuẩn của Dataverse, thêm cột `jas_balance` (công nợ) |
| Chứng từ đang mở | `jas_sales_header` / `jas_sales_line` | Đơn bán hàng (nháp) |
| | `jas_purchase_header` / `jas_purchase_line` | Phiếu nhập hàng (nháp) |
| | `jas_attendance_header` / `jas_attendance_line` | Phiếu điểm danh (nháp) |
| Chứng từ đã ghi sổ | `jas_posted_sales_header` / `jas_posted_sales_line` | Đơn bán đã khóa sổ (dòng gói học = 1 lượt đăng ký) |
| | `jas_posted_purchase_header` / `jas_posted_purchase_line` | Phiếu nhập đã khóa sổ |
| Sổ cái (ledger) | `jas_item_ledger_entry` | Bút toán tồn kho họa cụ |
| | `jas_value_entry` | Bút toán giá trị (giá vốn/doanh thu) |
| | `jas_session_ledger_entry` | Bút toán buổi học (mua buổi / điểm danh trừ buổi) |
| | `jas_student_ledger_entry` | Bút toán công nợ học viên (ghi nợ/thu tiền/hoàn tiền) |

### 2.2. Quy ước chung cho bảng master data
- Cột khóa chính hiển thị (`Primary Name Attribute`) luôn là **mã tự sinh** (`jas_no`, ví dụ `GV-00001`, `SH-00001`) — được thiết lập cố định lúc tạo bảng và **không thể đổi sau khi tạo** (giới hạn nền tảng Dataverse, không có API/UI hỗ trợ).
  - Vì lý do này, mọi màn hình hiển thị **tên thân thiện** (`jas_name`) thay vì mã, đều phải tự tra cứu qua một danh sách tên đã tải sẵn ở tầng ứng dụng (xem `resolveLookupName` trong mã nguồn từng trang) — không dựa vào cơ chế hiển thị mặc định của lookup.
- Ngừng dùng/kích hoạt lại dùng cơ chế `statecode`/`statuscode` có sẵn của Dataverse — không tạo cột trạng thái riêng.

### 2.3. Vòng đời chứng từ (Document → Post → Posted + Ledger)

```mermaid
flowchart LR
    A["Tạo chứng từ (Draft)\njas_sales_header/jas_purchase_header/jas_attendance_header"] --> B["Ghi sổ (Post)\ngọi Custom API tương ứng"]
    B --> C["Chứng từ Posted\n(bất biến, khóa sửa/xóa)"]
    B --> D["Bút toán Sổ Cái\n(Item/Value/Session/Student Ledger)"]
    D --> E["Số liệu cache cập nhật\n(tồn kho, buổi còn lại, công nợ)"]
```

Cột `jas_posting_state` (`Draft`/`Posting`/`Posted`/`PostingFailed`) trên các bảng header là cờ khóa idempotency — plugin set `Posting` ngay khi bắt đầu, tận dụng row-lock của Dataverse để chặn bấm ghi sổ 2 lần liên tiếp (double-click).

## 3. Custom API & Plugin (C#)

Mỗi nghiệp vụ ghi sổ chạy trong **1 transaction database thật** — nếu có lỗi giữa chừng, mọi thay đổi (kể cả việc set `Posting`) được rollback hoàn toàn.

| Custom API | Bound tới | Plugin | Logic chính |
|---|---|---|---|
| `jas_PostSalesOrder` | `jas_sales_header` | `PostSalesOrderPlugin` | Kiểm tồn kho mọi dòng họa cụ (kể cả cấp miễn phí) → tạo Posted Header/Lines → dòng gói học: tạo lượt đăng ký mới (remaining = số buổi gói, trạng thái Đang học) + bút toán Session Ledger (Mua buổi) → dòng họa cụ: bút toán Item/Value Ledger, trừ tồn kho → tính công nợ phải thu (không tính phần cấp miễn phí), cập nhật `jas_balance` |
| `jas_PostPurchase` | `jas_purchase_header` | `PostPurchasePlugin` | Mỗi dòng: bút toán Item/Value Ledger (nhập kho), cộng tồn kho, cập nhật giá vốn theo giá nhập gần nhất |
| `jas_PostAttendance` | `jas_attendance_header` | `PostAttendancePlugin` | Chỉ xử lý dòng có mặt; kiểm lượt đăng ký Đang học + còn buổi (hoặc buổi học thử/học nợ) + chưa trùng (mã trùng = lượt đăng ký + ngày + ca); dòng lỗi → bỏ qua dòng đó, không hủy cả phiếu; dòng hợp lệ → bút toán Session Ledger (Điểm danh, -1 buổi), trừ buổi còn lại, tự chuyển Hoàn thành nếu hết buổi (và không bật học nợ); stamp kèm ca học/giáo viên/trợ giảng lên bút toán để tra cứu sau này |
| `jas_MarkAsPaid` | `jas_posted_sales_header` | `MarkAsPaidPlugin` | Nhận số tiền thu (hỗ trợ thu từng phần, gọi nhiều lần) → bút toán Student Ledger (Thu tiền), cập nhật trạng thái thanh toán, giảm công nợ |
| `jas_ChangeLearningStatus` | `jas_posted_sales_line` | `ChangeLearningStatusPlugin` | Đổi trạng thái học (chỉ Đang học/Tạm ngưng/Đã hủy — không cho set Hoàn thành thủ công), không đụng đến số buổi còn lại |
| `jas_Reconcile` (unbound) | — | `ReconcilePlugin` | Tính lại số liệu cache (tồn kho, buổi còn lại, công nợ) từ tổng sổ cái, theo phạm vi Tất cả/Họa cụ/Học viên/Đăng ký |

**Chống trùng lặp (idempotency) dù đã có transaction thật**: transaction chỉ đảm bảo 1 lần gọi là atomic, không tự chặn 2 lần gọi độc lập — vẫn cần thêm (1) cờ `jas_posting_state` + row-lock, (2) Alternate Key ở tầng DB cho bút toán điểm danh (`jas_dedup_key` trên `jas_session_ledger_entry`).

**Giới hạn nền tảng đã xác nhận qua kiểm thử thực tế**: response body của cả 6 Custom API luôn trả `OutputParameters = null` bất kể thành công hay thất bại — nguyên nhân là các plugin đăng ký ở giai đoạn PostOperation (do giai đoạn Main Operation chuẩn theo tài liệu Microsoft không thực thi được trong môi trường này). Vì vậy mọi trang GenUX gọi Custom API đều phải dựa vào **HTTP status** (200 = thành công, 4xx kèm thông điệp lỗi nghiệp vụ = thất bại) thay vì đọc nội dung phản hồi.

## 4. Các trang GenUX (10 trang)

| Trang | Tệp mã nguồn | Chức năng chính |
|---|---|---|
| Bảng Điều Khiển (Role Center) | `role-center.tsx` | KPI tổng quan, chứng từ cần xử lý, cảnh báo sắp hết buổi |
| Đơn Bán Hàng | `sales-order-card.tsx` | Tạo/sửa/ghi sổ đơn bán (khóa học + họa cụ) |
| Phiếu Nhập Họa Cụ | `purchase-card.tsx` | Tạo/sửa/ghi sổ phiếu nhập họa cụ |
| Lịch Sử Điểm Danh | `attendance.tsx` | Tra cứu lịch sử điểm danh theo ngày/ca (chỉ đọc — điểm danh thật thực hiện ở Hồ Sơ Học Viên) |
| Hồ Sơ Học Viên | `student.tsx` | Quản lý học viên + popup Điểm danh + 4 tab tra cứu (công nợ, đăng ký, sổ buổi học, lịch sử mua hàng) |
| Họa Cụ | `item.tsx` | Quản lý danh mục họa cụ, tồn kho, giá vốn/giá bán |
| Chứng Từ Đã Ghi Sổ | `posted-documents.tsx` | Tra cứu đơn bán/phiếu nhập đã khóa sổ + thao tác Thu tiền/Đổi trạng thái học |
| Sổ Cái | `entries.tsx` | 4 sổ cái chỉ đọc + nút Đối Soát (chỉ Admin có quyền thực thi) |
| Thống Kê | `statistics.tsx` | Báo cáo doanh thu/học viên/công nợ |
| Thiết Lập | `setup.tsx` | CRUD 4 danh mục (Loại Lớp Học, Gói Học, Ca Học, Giáo Viên) + Cấu Hình chung |

### Sitemap (điều hướng)

```mermaid
flowchart TB
    subgraph Main["Area: Main"]
        direction TB
        G1["Tổng Quan\n(Role Center, Thống Kê)"]
        G2["Vận Hành\n(Đơn Bán Hàng, Phiếu Nhập Họa Cụ, Lịch Sử Điểm Danh)"]
        G3["Học Viên\n(Hồ Sơ Học Viên)"]
        G4["Họa Cụ"]
        G5["Chứng Từ Đã Ghi Sổ\n(Chứng Từ Đã Ghi Sổ, Sổ Cái)"]
    end
    subgraph Admin["Area: Admin Center"]
        G6["Thiết Lập"]
    end
```

Mỗi mục điều hướng có icon riêng phù hợp với chức năng (ví dụ: hồ sơ học viên dùng icon người, đơn bán hàng dùng icon hóa đơn, thiết lập dùng icon bánh răng).

## 5. Phân quyền

| Bảng/API | Admin | FrontDesk/Staff |
|---|---|---|
| Danh mục (loại lớp/gói học/ca học/họa cụ/giáo viên) | Toàn quyền | Chỉ đọc |
| Học viên (`contact`) | Toàn quyền | Toàn quyền |
| Chứng từ đang mở (đơn bán/phiếu nhập/phiếu điểm danh) | Toàn quyền | Toàn quyền |
| Chứng từ đã ghi sổ | Chỉ đọc | Chỉ đọc |
| Sổ cái (4 bảng `*_entry`) | Chỉ đọc | Chỉ đọc |
| Thực thi `jas_Post*` (ghi sổ) | Có | Có |
| Thực thi `jas_MarkAsPaid`, `jas_ChangeLearningStatus` | Có | Có |
| Thực thi `jas_Reconcile` (Đối Soát) | Có | **Không** |

Nguyên tắc nền tảng: chứng từ Đã Ghi Sổ và Sổ Cái **không ai có quyền Tạo/Sửa trực tiếp** — chỉ có thể ghi qua Custom API tương ứng, được thực thi (enforce) thật ở tầng nền tảng Dataverse, không chỉ ẩn nút trên giao diện.

## 6. An toàn thao tác (confirm dialog)

Các hành động khó hoàn tác đều có bước xác nhận trước khi thực hiện:

- **Ghi sổ đơn bán / phiếu nhập**: hiển thị hộp thoại xác nhận tóm tắt số dòng/tổng tiền, kèm cảnh báo nếu phát hiện bất thường (số lượng/giá vốn bằng 0, chưa nhập nhà cung cấp, có dòng cấp miễn phí, tổng tiền bằng 0) — vì sau khi ghi sổ, chứng từ khóa và không sửa/xóa dòng được nữa.
- **Xóa dòng** trên đơn bán/phiếu nhập: luôn có hộp thoại xác nhận riêng.
- **Thu tiền / Đổi trạng thái học / Đối Soát**: đã yêu cầu nhập thông tin (số tiền, trạng thái mới, phạm vi) trong hộp thoại trước khi xác nhận — tự thân đã là một bước xác nhận.
- **Ngừng dùng** học viên/họa cụ/giáo viên/danh mục: có hộp thoại xác nhận ngắn (vì đây là thao tác có thể hoàn tác bằng cách kích hoạt lại, nên chỉ cảnh báo nhẹ, không chặn bằng chứng từ khóa).

## 6.5. Tải dữ liệu danh sách & làm mới thủ công

Hầu hết các trang danh sách/dashboard dùng chung một mẫu cache phía client: dữ liệu được lưu vào `window.__pp*Cache` (một khóa theo từng trang/query) ngay lần tải đầu tiên trong phiên trình duyệt, và các lần chuyển trang qua lại sau đó đọc thẳng từ cache thay vì gọi lại Dataverse — giúp điều hướng nhanh nhưng có thể hiển thị dữ liệu cũ nếu có thay đổi xảy ra ở nơi khác trong cùng phiên. Mỗi trang có cache kiểu này đều có kèm:
- Nút **Làm mới** (icon `ArrowClockwiseRegular`/`ArrowSyncRegular`) — xóa cache + gọi lại truy vấn.
- Nhãn thời gian tương đối bên cạnh (`useRelativeTimeLabel`, hàm dùng chung được sao chép riêng vào từng tệp theo đúng quy ước "không import chéo file" của kiến trúc này) — hiển thị "vừa xong"/"X giây trước"/"X phút trước"/"X giờ trước"/"X ngày trước", tự cập nhật mỗi 15 giây qua `setInterval`.
- Một khóa cache thời điểm tải đi kèm (ví dụ `<cacheKey>_at`) được ghi `Date.now()` cùng lúc với khóa dữ liệu, để nhãn phản ánh đúng thời điểm dữ liệu thực sự được tải, không phải thời điểm trang được mở.

## 7. Ghi chú kỹ thuật cho người kế thừa/mở rộng hệ thống

- Toàn bộ trang được sinh và triển khai qua `pac model genpage` (React 17 + Fluent UI v9), mã nguồn nằm ở `joiart-genux/`.
- Schema Dataverse định nghĩa dưới dạng JSON tại `dataverse/schema/`, triển khai qua các script PowerShell trong `scripts/` (`deploy-tables.ps1`, `deploy-procode-schema.ps1` cho cột/lookup thêm vào bảng đã tồn tại, `deploy-plugin-package.ps1`, `deploy-custom-apis.ps1`, `deploy-security-roles.ps1`).
- Plugin C# nằm ở `plugins/JoiArtStudio.Plugins/`.
- Chỉnh sửa sitemap (thêm/gộp nhóm điều hướng, icon) yêu cầu export solution unmanaged, sửa trực tiếp khối `<SiteMap>` trong `customizations.xml`, rồi import lại — không có API ghi trực tiếp sitemap.
- **Lưu ý khi import solution hoặc cập nhật gói plugin**: cả 2 thao tác này có thể vô tình tắt (Disable) toàn bộ 6 bước xử lý plugin (`SdkMessageProcessingStep`) — luôn kiểm tra và bật lại sau mỗi lần import/deploy plugin.
