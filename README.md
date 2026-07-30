# JoiArt Studio — Hệ Thống Quản Lý Lớp Học

Đây là tài liệu (wiki) cho hệ thống quản lý vận hành trung tâm nghệ thuật **JoiArt Studio**: quản lý học viên, điểm danh lớp học, bán/mua hàng, công nợ và báo cáo. Hệ thống được xây dựng trên nền **Microsoft Power Platform / Dataverse** (model-driven app + trang GenUX + Dataverse Plugin), thay thế hoàn toàn phiên bản Canvas App trước đây.

> Tài liệu này chỉ mô tả kiến trúc **pro-code hiện tại** (model-driven app + GenUX + Plugin C#). Không đề cập lại chi tiết triển khai Canvas App cũ.

## Mục lục

| Tài liệu | Dành cho | Nội dung |
|---|---|---|
| [01 — Yêu Cầu Nghiệp Vụ (Requirements)](01-requirements.md) | Chủ trung tâm, người phụ trách nghiệp vụ | Yêu cầu chức năng, quy tắc nghiệp vụ, phạm vi hệ thống |
| [02 — Kiến Trúc & Thiết Kế (Design)](02-design.md) | Người phát triển, quản trị hệ thống | Mô hình dữ liệu, Custom API/Plugin, các trang GenUX, phân quyền |
| [03 — Hướng Dẫn Sử Dụng (User Guide)](03-user-guide.md) | Nhân viên phụ trách điểm danh / lễ tân, quản lý trung tâm | Hướng dẫn từng nghiệp vụ theo use case, có ảnh chụp luồng thao tác |

## Hệ thống dùng để làm gì?

JoiArt Studio là phần mềm quản lý cho một trung tâm dạy vẽ/nghệ thuật, giúp:

- Quản lý hồ sơ học viên, gói học đã đăng ký, số buổi còn lại.
- **Điểm danh lớp học** hằng ngày — chọn ca học, giáo viên phụ trách/trợ giảng, tự động trừ buổi.
- Quản lý giáo viên (toàn thời gian/bán thời gian).
- Bán khóa học và họa cụ (văn phòng phẩm/vật liệu vẽ) cho học viên, theo dõi công nợ.
- Nhập hàng họa cụ từ nhà cung cấp, theo dõi tồn kho và giá vốn.
- Xem báo cáo doanh thu, cảnh báo học viên sắp hết buổi, công nợ chưa thu.

## Truy cập hệ thống

- Ứng dụng: **JoiArt Studio Pro** (model-driven app trên Power Apps/Dynamics 365).
- Đăng nhập bằng tài khoản Microsoft 365 được cấp trong trung tâm.
- Có 2 khu vực điều hướng (Area): **Main** (nghiệp vụ hằng ngày) và **Admin Center** (thiết lập, chỉ nên dùng bởi quản lý).

## Vai trò người dùng

| Vai trò | Mô tả | Quyền chính |
|---|---|---|
| **Admin** | Chủ trung tâm / quản lý cấp cao | Toàn quyền, bao gồm Đối Soát (Reconcile) số liệu hệ thống |
| **FrontDesk / Staff** | Nhân viên lễ tân, phụ trách điểm danh | Quản lý học viên, điểm danh, bán/mua hàng, xem báo cáo — không có quyền Đối Soát |

Xem chi tiết ma trận phân quyền trong [02 — Kiến Trúc & Thiết Kế](02-design.md#phân-quyền).
