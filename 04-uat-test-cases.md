# Bộ Test Case UAT (User Acceptance Testing)

← [Về trang chủ](README.md)

Tài liệu này dành cho **người kiểm thử nghiệm thu (UAT)** — không cần biết code, chỉ cần
làm theo từng bước và so sánh với "Kết quả mong đợi". Bộ test case bám sát các nghiệp vụ đã
mô tả tại [01 — Yêu Cầu Nghiệp Vụ](01-requirements.md) và các bước thao tác tại
[03 — Hướng Dẫn Sử Dụng](03-user-guide.md) — khi cần xem lại thao tác chi tiết hơn, tra theo
số mục được ghi chú trong ngoặc ở mỗi nhóm test case.

## Cách dùng tài liệu này

Mỗi test case gồm các trường:

| Trường | Ý nghĩa |
|---|---|
| **ID** | Mã test case, dạng `UAT-<nhóm>-<số>` |
| **Vai trò** | Tài khoản cần dùng để chạy test case (Admin / FrontDesk / Cả hai) |
| **Điều kiện tiên quyết** | Dữ liệu/trạng thái cần có sẵn trước khi bắt đầu |
| **Bước thực hiện** | Các thao tác cụ thể trên hệ thống |
| **Dữ liệu test** | Gợi ý dữ liệu mẫu dùng để chạy test case |
| **Kết quả mong đợi** | Hệ thống phải phản hồi đúng như mô tả |
| **Kết quả thực tế** | Người kiểm thử tự điền khi chạy |
| **Đạt/Không đạt** | Người kiểm thử tự đánh dấu ☐ Đạt / ☐ Không đạt |
| **Ghi chú** | Người kiểm thử tự điền (lỗi gặp phải, ảnh chụp màn hình...) |

**Quy ước dữ liệu test — quan trọng**: mọi học viên/giáo viên/gói học dùng để chạy UAT phải
có **tên bắt đầu bằng "TEST"** (ví dụ "Nguyễn Văn TEST", "TEST Acrylic 24 buổi", "GV TEST
Toàn Thời Gian") — **tuyệt đối không dùng dữ liệu học viên thật** để tránh ảnh hưởng số liệu
kinh doanh thật (công nợ, tồn kho, doanh thu). Tên gói học/học phí có thể tham khảo bảng giá
thật của trung tâm (Joyful Colors, Mixed Media Painting, Foundation Studio, Advanced Studio)
để dữ liệu test trông thực tế hơn, miễn là tên học viên vẫn có tiền tố TEST. Sau khi UAT
xong, nên dọn dẹp toàn bộ dữ liệu TEST đã tạo (hoặc nhờ đội kỹ thuật dọn) trước khi hệ thống
đi vào vận hành thật.

**Cần 2 tài khoản để chạy đầy đủ bộ test case này**: 1 tài khoản vai trò **Admin**, 1 tài
khoản vai trò **FrontDesk/Staff** — nhiều test case (đặc biệt nhóm `UAT-PERM`) yêu cầu so
sánh hành vi giữa 2 vai trò.

---

## Mục lục nhóm test case

| Nhóm | Chủ đề | Số lượng | Tham chiếu |
|---|---|---|---|
| [UAT-STU](#uat-stu--quản-lý-học-viên) | Quản lý học viên | 8 | User Guide mục 2 |
| [UAT-DD](#uat-dd--điểm-danh) | Điểm danh | 18 | User Guide mục 3 |
| [UAT-SO](#uat-so--đơn-bán-hàng) | Đơn Bán Hàng | 15 | User Guide mục 4 |
| [UAT-PC](#uat-pc--phiếu-nhập-họa-cụ) | Phiếu Nhập Họa Cụ | 9 | User Guide mục 5 |
| [UAT-PR](#uat-pr--bảng-lương) | Bảng Lương | 8 | User Guide mục 6 |
| [UAT-CF](#uat-cf--dòng-tiền-mặt) | Dòng Tiền Mặt | 7 | User Guide mục 10 |
| [UAT-SET](#uat-set--thiết-lập-danh-mục) | Thiết Lập danh mục | 10 | User Guide mục 7, 11 |
| [UAT-PD](#uat-pd--chứng-từ-đã-ghi-sổ) | Chứng Từ Đã Ghi Sổ | 8 | User Guide mục 8, 9 |
| [UAT-LED](#uat-led--sổ-cái) | Sổ Cái | 9 | Design mục 4 (`entries.tsx`) |
| [UAT-STAT](#uat-stat--thống-kê) | Thống Kê | 4 | User Guide mục 10 |
| [UAT-RC](#uat-rc--role-center--bảng-điều-khiển) | Role Center | 3 | User Guide mục 10 |
| [UAT-PERM](#uat-perm--phân-quyền-bất-biến-chứng-từ--an-toàn-thao-tác) | Phân quyền & an toàn thao tác | 10 | Design mục 5, 6 |

**Tổng cộng: 109 test case.**

---

## UAT-STU — Quản lý học viên

*(Vào: Học Viên → Hồ Sơ Học Viên — xem User Guide mục 2)*

#### UAT-STU-01 — Thêm học viên mới thành công
- **Vai trò**: Cả hai (Admin, FrontDesk)
- **Điều kiện tiên quyết**: Không có
- **Bước thực hiện**: Bấm **Thêm** ở góc trên danh sách bên trái → nhập Họ và tên "Nguyễn Văn TEST" + số điện thoại/email/ngày sinh/giới tính/địa chỉ/ghi chú tùy chọn → bấm **Lưu**.
- **Dữ liệu test**: Họ tên "Nguyễn Văn TEST"
- **Kết quả mong đợi**: Học viên mới xuất hiện ngay trong danh sách bên trái, mở được hồ sơ chi tiết.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-STU-02 — Thêm học viên thiếu Họ và tên
- **Vai trò**: Cả hai
- **Bước thực hiện**: Bấm **Thêm**, để trống Họ và tên, bấm **Lưu**.
- **Kết quả mong đợi**: Không lưu được (Họ và tên là trường bắt buộc) — hệ thống báo lỗi hoặc chặn nút Lưu.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-STU-03 — Xem hồ sơ học viên đầy đủ thông tin
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Học viên TEST đã có ít nhất 1 gói học đang hoạt động và 1 lượt điểm danh
- **Bước thực hiện**: Chọn học viên TEST trong danh sách.
- **Kết quả mong đợi**: Khung bên phải hiển thị đúng: tổng số buổi còn lại (cộng tất cả gói đang hoạt động), công nợ, trạng thái hoạt động, 2 nút **Điểm danh**/**Tạo đơn bán hàng**, và đúng 4 tab **Sổ Buổi Học** (mặc định)/**Ghi Danh**/**Công Nợ**/**Lịch Sử Mua Họa Cụ**.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-STU-04 — Ngừng hoạt động học viên
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở hồ sơ học viên TEST → bấm **Ngừng hoạt động**.
- **Kết quả mong đợi**: Hộp thoại xác nhận hiện ra trước khi thực hiện; sau khi xác nhận, học viên biến mất khỏi danh sách mặc định (không bật "Hiện đã ngừng hoạt động").
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-STU-05 — Kích hoạt lại học viên đã ngừng hoạt động
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Có học viên TEST đã ngừng hoạt động (UAT-STU-04)
- **Bước thực hiện**: Bật công tắc **"Hiện đã ngừng hoạt động"** → mở học viên đó → bấm **Kích hoạt lại**.
- **Kết quả mong đợi**: Học viên trở lại danh sách mặc định, hoạt động bình thường.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-STU-06 — Nút "Điểm danh" mở đúng học viên đang chọn
- **Vai trò**: Cả hai
- **Bước thực hiện**: Chọn học viên TEST → bấm **Điểm danh**.
- **Kết quả mong đợi**: Popup "Điểm danh — [tên học viên]" mở ra đúng tên học viên vừa chọn.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-STU-07 — Nút "Tạo đơn bán hàng" gắn sẵn đúng học viên
- **Vai trò**: Cả hai
- **Bước thực hiện**: Chọn học viên TEST → bấm **Tạo đơn bán hàng**.
- **Kết quả mong đợi**: Mở Đơn Bán Hàng mới, học viên đã gắn sẵn đúng người vừa chọn, không có cách nào đổi sang học viên khác trên đơn này.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-STU-08 — FrontDesk có toàn quyền quản lý học viên
- **Vai trò**: FrontDesk
- **Bước thực hiện**: Lặp lại UAT-STU-01 (Thêm), UAT-STU-04 (Ngừng hoạt động) bằng tài khoản FrontDesk.
- **Kết quả mong đợi**: Cả 2 thao tác đều thực hiện được bình thường — bảng `contact` là "Toàn quyền" cho cả 2 vai trò theo ma trận phân quyền (Design §5).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

---

## UAT-DD — Điểm danh

*(Vào: Học Viên → Hồ Sơ Học Viên → chọn học viên → Điểm danh — xem User Guide mục 3, "nghiệp vụ quan trọng nhất")*

#### UAT-DD-01 — Điểm danh thông thường, học viên chỉ có 1 gói đang hoạt động
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Học viên TEST có đúng 1 gói "Đang học", còn buổi > 0
- **Bước thực hiện**: Bấm **Điểm danh** → hệ thống tự chọn sẵn gói (chỉ có 1) → chọn **Ca học** + **Giáo viên phụ trách** → bấm **Điểm danh**.
- **Kết quả mong đợi**: Thông báo **"Đã điểm danh cho [tên]. Số buổi còn lại: X"**, X giảm đúng 1 so với trước.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-02 — Điểm danh khi học viên có nhiều gói đang hoạt động
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Học viên TEST có ≥ 2 gói "Đang học" còn buổi
- **Bước thực hiện**: Bấm **Điểm danh** → chọn thủ công 1 trong các gói ở **Khóa đã mua** → chọn Ca học + Giáo viên → bấm **Điểm danh**.
- **Kết quả mong đợi**: Đúng gói được chọn bị trừ buổi, các gói khác không đổi.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-03 — Nút "Điểm danh" bị mờ khi thiếu trường bắt buộc
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở popup Điểm danh, để trống Ca học hoặc Giáo viên phụ trách.
- **Kết quả mong đợi**: Nút **Điểm danh** bị mờ (disabled), không bấm được.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-04 — Điểm danh có chọn Trợ giảng
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Có ≥ 2 giáo viên TEST
- **Bước thực hiện**: Chọn Giáo viên phụ trách là GV1 → chọn Trợ giảng là GV2 (khác GV1) → Điểm danh.
- **Kết quả mong đợi**: Thành công; danh sách Trợ giảng không cho chọn trùng với Giáo viên phụ trách đã chọn.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-05 — Điểm danh 2 ca khác nhau cùng ngày, cùng gói
- **Vai trò**: Cả hai
- **Bước thực hiện**: Điểm danh học viên TEST với Ca sáng → thành công. Lặp lại ngay trong ngày với **Ca chiều** (khác ca đầu), cùng gói.
- **Kết quả mong đợi**: Cả 2 lần đều thành công, trừ buổi 2 lần (không bị coi là trùng vì khác Ca học).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-06 — Điểm danh trùng (idempotency)
- **Vai trò**: Cả hai
- **Bước thực hiện**: Điểm danh học viên TEST với gói X, ngày Y, ca Z → thành công. Lặp lại **y hệt** gói X + ngày Y + ca Z.
- **Kết quả mong đợi**: Thông báo **"Hệ thống đã bỏ qua yêu cầu này (có thể đã điểm danh gói này hôm nay, hết buổi, hoặc đang tạm ngưng)..."**, số buổi còn lại **không đổi** so với sau lần điểm danh thứ nhất.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-07 — Điểm danh buổi học thử
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Thiết Lập → Cấu Hình đã chọn sẵn 1 gói học thử
- **Bước thực hiện**: Mở popup Điểm danh → bật công tắc **"Buổi học thử"** → chọn Ca học + Giáo viên phụ trách → Điểm danh.
- **Kết quả mong đợi**: Ghi nhận có mặt thành công, **không trừ vào bất kỳ gói học thật nào** của học viên (kiểm tra số buổi còn lại các gói thật không đổi).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-08 — Công tắc "Buổi học thử" bị mờ khi chưa cấu hình gói học thử
- **Vai trò**: Admin (để cấu hình trước), Cả hai (để kiểm tra)
- **Bước thực hiện**: Ở Thiết Lập → Cấu Hình, **bỏ chọn** gói học thử (để trống) → mở popup Điểm danh cho học viên bất kỳ.
- **Kết quả mong đợi**: Công tắc "Buổi học thử" bị mờ/không bật được. *(Nhớ cấu hình lại gói học thử sau khi test xong để không ảnh hưởng vận hành thật.)*
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-09 — Điểm danh khi hết buổi, "Cho phép học nợ" đang tắt
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: "Cho phép học nợ" đang **tắt**; học viên TEST có gói đã hết buổi (remaining = 0), không có gói nào khác đang hoạt động
- **Bước thực hiện**: Mở popup Điểm danh cho học viên đó.
- **Kết quả mong đợi**: Thông báo **"Học viên không có gói học nào đang hoạt động và còn buổi"**, không điểm danh được.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-10 — Điểm danh học nợ khi "Cho phép học nợ" đang bật
- **Vai trò**: Admin (bật cấu hình), Cả hai (điểm danh)
- **Điều kiện tiên quyết**: Thiết Lập → Cấu Hình đã **bật** "Cho phép học nợ"; học viên TEST có gói remaining = 0
- **Bước thực hiện**: Điểm danh học viên đó với gói đã hết buổi.
- **Kết quả mong đợi**: Vẫn điểm danh được, số buổi còn lại hiển thị **số âm** (ví dụ "-1 buổi"), gói học vẫn giữ trạng thái "Đang học" (không tự chuyển "Hoàn thành").
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-11 — Xem Sổ Buổi Học trên hồ sơ học viên
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở hồ sơ học viên TEST đã có vài lượt điểm danh → tab **Sổ Buổi Học**.
- **Kết quả mong đợi**: Danh sách đúng, có cột **Ca**, **Giáo Viên**, **Trợ Giảng**, sắp xếp mới nhất trước.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-12 — Tra cứu Lịch Sử Điểm Danh toàn hệ thống theo ngày/ca
- **Vai trò**: Cả hai
- **Bước thực hiện**: Vào Vận Hành → **Lịch Sử Điểm Danh** → lọc theo 1 ngày + 1 ca cụ thể đã biết có điểm danh.
- **Kết quả mong đợi**: Hiển thị đúng danh sách học viên đã điểm danh đúng ngày/ca đó, kèm giáo viên/trợ giảng phụ trách.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-13 — Hủy điểm danh qua popup "Chi tiết"
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Có 1 lượt điểm danh (loại "Điểm Danh", chưa bị hủy) ghi sổ **hôm nay**
- **Bước thực hiện**: Vào tab **Sổ Buổi Học** → bấm **Chi tiết** trên dòng cần hủy → trong popup chi tiết vừa mở, bấm nút **Hủy điểm danh** (nút viền đỏ, tách biệt khỏi nút Đóng) → xác nhận hộp thoại *"Hủy buổi điểm danh [mã]? Buổi học sẽ được hoàn lại vào số buổi còn lại."*
- **Kết quả mong đợi**: Số buổi còn lại của gói tăng lại +1; dòng gốc trong Sổ Buổi Học vẫn còn, chuyển sang trạng thái "Đã bị hủy"; popup tự đóng sau khi hủy thành công.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-14 — Entry đã "Đã bị hủy" không còn nút Hủy điểm danh
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Có 1 entry đã hủy (kết quả của UAT-DD-13)
- **Bước thực hiện**: Bấm **Chi tiết** trên đúng dòng đã bị hủy đó.
- **Kết quả mong đợi**: Popup chi tiết mở ra bình thường nhưng **không hiển thị** nút "Hủy điểm danh" (chỉ có nút Đóng) — tránh hủy 2 lần.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-15 — FrontDesk hủy điểm danh trong ngày hôm nay
- **Vai trò**: FrontDesk
- **Bước thực hiện**: Lặp lại UAT-DD-13 với 1 entry điểm danh ghi sổ **hôm nay**, đăng nhập bằng tài khoản FrontDesk.
- **Kết quả mong đợi**: Hủy thành công.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-16 — FrontDesk bị chặn hủy điểm danh của ngày trước đó
- **Vai trò**: FrontDesk
- **Điều kiện tiên quyết**: Có 1 entry điểm danh ghi sổ **không phải hôm nay** (ví dụ hôm qua)
- **Bước thực hiện**: Đăng nhập FrontDesk → mở Chi tiết entry đó → bấm Hủy điểm danh (nếu nút hiển thị) hoặc xác nhận nút bị ẩn/mờ.
- **Kết quả mong đợi**: Bị chặn — hoặc nút không hiển thị, hoặc bấm vào nhận thông báo lỗi rõ ràng nêu lý do (không phải lỗi kỹ thuật khó hiểu).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-17 — Admin hủy điểm danh của bất kỳ ngày nào
- **Vai trò**: Admin
- **Điều kiện tiên quyết**: Entry điểm danh của một ngày trong quá khứ (không phải hôm nay)
- **Bước thực hiện**: Đăng nhập Admin → lặp lại UAT-DD-13 trên entry đó.
- **Kết quả mong đợi**: Hủy thành công dù không phải ngày hôm nay.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-18 — Hủy điểm danh đưa gói học từ "Hoàn thành" quay lại "Đang học"
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Gói học TEST vừa điểm danh hết buổi cuối cùng, đã tự chuyển "Hoàn thành"
- **Bước thực hiện**: Hủy điểm danh đúng lượt vừa khiến gói "Hoàn thành".
- **Kết quả mong đợi**: Gói học tự quay lại trạng thái "Đang học" vì lại có buổi > 0.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

---

## UAT-SO — Đơn Bán Hàng

*(Vào: từ hồ sơ học viên → Tạo đơn bán hàng — xem User Guide mục 4)*

#### UAT-SO-01 — Tạo đơn bán hàng gắn sẵn đúng học viên
- **Vai trò**: Cả hai
- **Bước thực hiện**: Từ hồ sơ học viên TEST, bấm **Tạo đơn bán hàng**.
- **Kết quả mong đợi**: Đơn mới mở ra, học viên đã gắn sẵn, không đổi được sang học viên khác.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SO-02 — Thêm dòng Họa Cụ, đơn giá tự điền
- **Vai trò**: Cả hai
- **Bước thực hiện**: Bấm **Thêm dòng** → chọn loại **Họa Cụ** → chọn 1 họa cụ TEST → kiểm tra đơn giá tự điền theo giá bán lẻ → thử sửa lại đơn giá.
- **Kết quả mong đợi**: Đơn giá tự điền đúng giá bán lẻ, sửa tay được.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SO-03 — Dòng Họa Cụ "Cấp miễn phí"
- **Vai trò**: Cả hai
- **Bước thực hiện**: Thêm dòng Họa Cụ, số lượng 2 → tick **Cấp miễn phí**.
- **Kết quả mong đợi**: Dòng này **không cộng vào Số tiền phải thu**, nhưng sau khi ghi sổ vẫn trừ tồn kho đúng 2.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SO-04 — Thêm dòng Gói Học
- **Vai trò**: Cả hai
- **Bước thực hiện**: Thêm dòng, chọn loại **Gói Học** → chọn Loại lớp học → chọn Gói học cụ thể.
- **Kết quả mong đợi**: Giá/số buổi/thời hạn tự điền đúng theo cấu hình gói đã chọn.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SO-05 — Trộn nhiều dòng Họa Cụ + Gói Học trong cùng đơn
- **Vai trò**: Cả hai
- **Bước thực hiện**: Thêm ít nhất 1 dòng Gói Học và 2 dòng Họa Cụ khác nhau trong cùng 1 đơn.
- **Kết quả mong đợi**: Cả 3 dòng cùng tồn tại bình thường, Tổng tiền cộng đúng tất cả các dòng.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SO-06 — Nút "Nhận đủ tiền"
- **Vai trò**: Cả hai
- **Bước thực hiện**: Sau khi có Số tiền phải thu > 0, bấm **Nhận đủ tiền**.
- **Kết quả mong đợi**: Số tiền đã thu tự điền đúng bằng Số tiền phải thu.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SO-07 — Cảnh báo thu thiếu/thu dư
- **Vai trò**: Cả hai
- **Bước thực hiện**: Nhập Số tiền đã thu **thấp hơn** Số tiền phải thu → quan sát. Sau đó sửa thành **cao hơn** → quan sát lại.
- **Kết quả mong đợi**: Trường hợp thiếu hiện **"Thiếu X ₫"**; trường hợp dư hiện **"Dư X ₫"**, cạnh Trạng thái thanh toán.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SO-08 — Hộp thoại xác nhận trước khi ghi sổ
- **Vai trò**: Cả hai
- **Bước thực hiện**: Bấm **Ghi sổ đơn hàng**.
- **Kết quả mong đợi**: Hộp thoại xác nhận hiện ra, tóm tắt học viên/số dòng/tổng tiền/số tiền đã thu, kèm cảnh báo nếu có bất thường (thu thiếu/thu dư/có dòng cấp miễn phí/tổng tiền = 0).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SO-09 — Kết quả sau khi ghi sổ thành công
- **Vai trò**: Cả hai
- **Bước thực hiện**: Xác nhận Ghi sổ trên đơn có cả dòng Gói Học và Họa Cụ.
- **Kết quả mong đợi**: Đơn khóa (không sửa/xóa dòng được); mỗi dòng Gói Học thành 1 lượt đăng ký mới đủ buổi; tồn kho họa cụ giảm đúng số lượng; công nợ học viên tăng đúng Số tiền phải thu (không tính phần cấp miễn phí) trừ phần đã thu ngay.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SO-10 — Không ghi sổ được đơn chưa có dòng nào
- **Vai trò**: Cả hai
- **Bước thực hiện**: Tạo đơn mới, không thêm dòng nào, bấm Ghi sổ đơn hàng.
- **Kết quả mong đợi**: Bị chặn, không ghi sổ được.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SO-11 — Không ghi sổ được nếu Họa Cụ vượt tồn kho
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: 1 họa cụ TEST tồn kho hiện tại thấp (ví dụ = 1)
- **Bước thực hiện**: Thêm dòng bán họa cụ đó số lượng lớn hơn tồn kho (ví dụ 100) → thử Ghi sổ.
- **Kết quả mong đợi**: Bị chặn, thông báo rõ họa cụ nào vượt tồn kho.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SO-12 — Đảo ngược ghi sổ đơn bán thành công (Admin)
- **Vai trò**: Admin
- **Điều kiện tiên quyết**: Đơn bán TEST đã ghi sổ, **chưa có lượt đăng ký nào bị điểm danh**
- **Bước thực hiện**: Vào Chứng Từ Đã Ghi Sổ → mở đơn → bấm **Đảo ngược ghi sổ** → đọc kỹ hộp thoại xác nhận → xác nhận.
- **Kết quả mong đợi**: Tồn kho họa cụ hoàn lại; lượt đăng ký gói học trong đơn chuyển "Đã hủy"; công nợ học viên điều chỉnh lại đúng; đơn nháp gốc **mở khóa lại** để sửa/ghi sổ lại; bản ghi Đã Ghi Sổ gốc vẫn còn, đánh dấu "Đã đảo ngược".
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SO-13 — Đảo ngược bị chặn nếu đã điểm danh
- **Vai trò**: Admin
- **Điều kiện tiên quyết**: Đơn bán TEST đã ghi sổ, có 1 lượt đăng ký **đã điểm danh ít nhất 1 buổi**
- **Bước thực hiện**: Bấm **Đảo ngược ghi sổ** trên đơn đó.
- **Kết quả mong đợi**: Bị chặn, thông báo lỗi nêu rõ tên lượt đăng ký đang chặn — hướng dẫn phải Hủy điểm danh hết các buổi liên quan trước.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SO-14 — FrontDesk không thực hiện được Đảo ngược ghi sổ
- **Vai trò**: FrontDesk
- **Bước thực hiện**: Đăng nhập FrontDesk → mở 1 đơn bán đã ghi sổ → tìm nút Đảo ngược ghi sổ.
- **Kết quả mong đợi**: Nút không hiển thị, hoặc bấm vào nhận thông báo từ chối quyền rõ ràng.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SO-15 — Đơn đã đảo ngược hiển thị nhãn "Đã đảo ngược"
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Kết quả của UAT-SO-12
- **Bước thực hiện**: Mở lại đúng đơn đã đảo ngược đó trong Chứng Từ Đã Ghi Sổ.
- **Kết quả mong đợi**: Hiển thị nhãn "Đã đảo ngược" thay cho nút Đảo ngược ghi sổ.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

---

## UAT-PC — Phiếu Nhập Họa Cụ

*(Vào: Vận Hành → Phiếu Nhập Họa Cụ — xem User Guide mục 5)*

#### UAT-PC-01 — Tạo phiếu nhập mới
- **Vai trò**: Cả hai
- **Bước thực hiện**: Bấm **Phiếu mới** → nhập Nhà cung cấp (tùy chọn) + Ngày nhập.
- **Kết quả mong đợi**: Phiếu nháp tạo thành công, sẵn sàng thêm dòng.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PC-02 — Tạo phiếu nhập từ hồ sơ 1 họa cụ
- **Vai trò**: Cả hai
- **Bước thực hiện**: Vào Họa Cụ → mở 1 họa cụ TEST → bấm **Tạo phiếu mua họa cụ**.
- **Kết quả mong đợi**: Phiếu mới mở ra, đã có sẵn 1 dòng với đúng họa cụ đó.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PC-03 — Thêm nhiều dòng họa cụ khác nhau
- **Vai trò**: Cả hai
- **Bước thực hiện**: Thêm 3 dòng, mỗi dòng 1 họa cụ khác nhau, số lượng + giá vốn khác nhau.
- **Kết quả mong đợi**: Cả 3 dòng lưu đúng, không giới hạn số dòng.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PC-04 — Cảnh báo khi ghi sổ thiếu thông tin
- **Vai trò**: Cả hai
- **Bước thực hiện**: Để 1 dòng có số lượng hoặc giá vốn = 0, hoặc bỏ trống Nhà cung cấp → bấm **Đăng ký ghi sổ**.
- **Kết quả mong đợi**: Hộp thoại xác nhận cảnh báo rõ vấn đề trước khi cho ghi sổ tiếp.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PC-05 — Tồn kho và giá vốn cập nhật sau ghi sổ
- **Vai trò**: Cả hai
- **Bước thực hiện**: Ghi nhận tồn kho + giá vốn (last cost) hiện tại của 1 họa cụ TEST → ghi sổ phiếu nhập 10 đơn vị, giá vốn mới khác giá cũ.
- **Kết quả mong đợi**: Tồn kho tăng đúng +10; giá vốn cập nhật thành giá vừa nhập (last cost = giá nhập gần nhất).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PC-06 — Ghi sổ phiếu nhập tự động ghi khoản chi vào Dòng Tiền Mặt
- **Vai trò**: Cả hai
- **Bước thực hiện**: Ghi sổ 1 phiếu nhập → sang trang Dòng Tiền Mặt, bấm Làm mới.
- **Kết quả mong đợi**: Tổng Chi tăng đúng bằng tổng giá trị phiếu nhập vừa ghi sổ; giao dịch xuất hiện trong danh sách gần đây.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PC-07 — Đảo ngược ghi sổ phiếu nhập thành công (Admin)
- **Vai trò**: Admin
- **Điều kiện tiên quyết**: Phiếu nhập TEST đã ghi sổ, tồn kho các họa cụ trong phiếu **vẫn còn đủ** để trừ lại
- **Bước thực hiện**: Vào Chứng Từ Đã Ghi Sổ → mở phiếu → bấm **Đảo ngược ghi sổ** → xác nhận.
- **Kết quả mong đợi**: Tồn kho trừ lại đúng số đã nhập; khoản chi tương ứng trong Dòng Tiền Mặt được bù lại; phiếu nháp gốc mở khóa lại; bản ghi Đã Ghi Sổ gốc vẫn còn, đánh dấu "Đã đảo ngược".
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PC-08 — Đảo ngược bị chặn nếu tồn kho không đủ
- **Vai trò**: Admin
- **Điều kiện tiên quyết**: Phiếu nhập TEST đã ghi sổ 10 đơn vị 1 họa cụ, sau đó đã bán ra khiến tồn kho hiện tại < 10
- **Bước thực hiện**: Bấm **Đảo ngược ghi sổ** trên phiếu đó.
- **Kết quả mong đợi**: Bị chặn, thông báo rõ tên họa cụ đang thiếu tồn kho để trừ lại.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PC-09 — FrontDesk không thực hiện được Đảo ngược phiếu nhập
- **Vai trò**: FrontDesk
- **Bước thực hiện**: Đăng nhập FrontDesk → mở 1 phiếu nhập đã ghi sổ → tìm nút Đảo ngược ghi sổ.
- **Kết quả mong đợi**: Nút không hiển thị hoặc bị từ chối quyền khi bấm.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

---

## UAT-PR — Bảng Lương

*(Vào: Vận Hành → Bảng Lương — xem User Guide mục 6)*

#### UAT-PR-01 — Tạo bảng lương mới
- **Vai trò**: Cả hai
- **Bước thực hiện**: Bấm **Bảng lương mới** → chọn Giáo viên TEST + Kỳ lương + Ngày chi.
- **Kết quả mong đợi**: Bảng lương nháp tạo thành công, gắn đúng giáo viên đã chọn.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PR-02 — Dòng Lương cứng/Theo buổi tự gợi ý số tiền
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Giáo viên TEST đã cấu hình sẵn "Lương cứng mặc định"/"Đơn giá/buổi mặc định" ở Thiết Lập
- **Bước thực hiện**: Thêm dòng, chọn loại **Lương cứng** (hoặc **Theo buổi**).
- **Kết quả mong đợi**: Số tiền tự gợi ý đúng theo mức mặc định đã cấu hình; sửa tay được.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PR-03 — Dòng Thưởng
- **Vai trò**: Cả hai
- **Bước thực hiện**: Thêm dòng loại **Thưởng**, nhập số tiền dương.
- **Kết quả mong đợi**: Lưu thành công, cộng vào Tổng tiền.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PR-04 — Dòng Khấu trừ nhập số âm
- **Vai trò**: Cả hai
- **Bước thực hiện**: Thêm dòng loại **Khấu trừ**, nhập số tiền **âm**.
- **Kết quả mong đợi**: Cho phép nhập số âm (đây là loại dòng duy nhất trong toàn hệ thống cho phép số âm), trừ đúng vào Tổng tiền.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PR-05 — Nhiều loại dòng trong cùng 1 bảng lương
- **Vai trò**: Cả hai
- **Bước thực hiện**: Thêm 1 dòng Lương cứng + 1 dòng Thưởng + 1 dòng Khấu trừ (âm) cho cùng giáo viên.
- **Kết quả mong đợi**: Tổng tiền = Lương cứng + Thưởng + Khấu trừ (cộng đại số đúng, kể cả số âm).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PR-06 — Cảnh báo khi ghi sổ thiếu thông tin
- **Vai trò**: Cả hai
- **Bước thực hiện**: Để 1 dòng số tiền = 0 hoặc thiếu diễn giải → bấm **Đăng ký ghi sổ**.
- **Kết quả mong đợi**: Hộp thoại xác nhận cảnh báo rõ vấn đề.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PR-07 — Kết quả sau khi ghi sổ bảng lương
- **Vai trò**: Cả hai
- **Bước thực hiện**: Xác nhận Ghi sổ bảng lương hợp lệ.
- **Kết quả mong đợi**: Bảng lương khóa lại; 1 bút toán mới xuất hiện ở Sổ Nhân Viên đúng giáo viên; 1 khoản chi mới xuất hiện ở Dòng Tiền Mặt đúng số tiền.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PR-08 — Không có nghiệp vụ đảo ngược bảng lương
- **Vai trò**: Admin
- **Bước thực hiện**: Mở 1 bảng lương đã ghi sổ trong Chứng Từ Đã Ghi Sổ.
- **Kết quả mong đợi**: **Không có** nút Đảo ngược ghi sổ nào xuất hiện (khác với Đơn Bán Hàng/Phiếu Nhập Họa Cụ) — đúng theo phạm vi đã chốt không làm.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

---

## UAT-CF — Dòng Tiền Mặt

*(Vào: Tổng Quan → Dòng Tiền Mặt — xem User Guide mục 10)*

#### UAT-CF-01 — KPI Tổng Thu/Tổng Chi/Dòng Tiền Ròng
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở trang Dòng Tiền Mặt.
- **Kết quả mong đợi**: Hiển thị đúng 3 KPI của tháng hiện tại: Tổng Thu, Tổng Chi, Dòng Tiền Ròng (= Thu − Chi).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-CF-02 — Biểu đồ Thu/Chi theo tháng
- **Vai trò**: Cả hai
- **Bước thực hiện**: Quan sát biểu đồ trên trang Dòng Tiền Mặt.
- **Kết quả mong đợi**: Hiển thị đúng vài tháng gần nhất, có phân biệt Thu/Chi.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-CF-03 — Danh sách giao dịch gần đây
- **Vai trò**: Cả hai
- **Bước thực hiện**: Quan sát danh sách giao dịch gần đây.
- **Kết quả mong đợi**: Hiển thị đúng các giao dịch thu/chi gần nhất, đúng ngày/số tiền/nguồn.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-CF-04 — Thu tiền học viên phản ánh đúng vào Tổng Thu
- **Vai trò**: Cả hai
- **Bước thực hiện**: Ghi nhận Tổng Thu hiện tại → ghi sổ 1 đơn bán có thu tiền ngay (hoặc Đánh dấu đã thu tiền 1 đơn cũ) → quay lại Dòng Tiền Mặt, bấm **Làm mới**.
- **Kết quả mong đợi**: Tổng Thu tăng đúng bằng số tiền vừa thu.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-CF-05 — Mua hàng phản ánh đúng vào Tổng Chi
- **Vai trò**: Cả hai
- **Bước thực hiện**: Ghi nhận Tổng Chi hiện tại → ghi sổ 1 phiếu nhập họa cụ → Làm mới Dòng Tiền Mặt.
- **Kết quả mong đợi**: Tổng Chi tăng đúng bằng giá trị phiếu nhập.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-CF-06 — Trả lương phản ánh đúng vào Tổng Chi
- **Vai trò**: Cả hai
- **Bước thực hiện**: Ghi nhận Tổng Chi hiện tại → ghi sổ 1 bảng lương → Làm mới Dòng Tiền Mặt.
- **Kết quả mong đợi**: Tổng Chi tăng đúng bằng tổng bảng lương.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-CF-07 — Trang Dòng Tiền Mặt hoàn toàn chỉ đọc
- **Vai trò**: Cả hai
- **Bước thực hiện**: Rà soát toàn trang.
- **Kết quả mong đợi**: Không có bất kỳ nút Thêm/Sửa/Nhập tay giao dịch nào — toàn bộ số liệu chỉ đến từ các chứng từ đã ghi sổ nguồn (thu tiền/mua hàng/lương).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

---

## UAT-SET — Thiết Lập danh mục

*(Vào: chuyển Area sang Admin Center → Thiết Lập — xem User Guide mục 7, 11)*

#### UAT-SET-01 — CRUD Loại Lớp Học
- **Vai trò**: Admin
- **Bước thực hiện**: Tab Loại Lớp Học → Thêm 1 loại lớp TEST (tên, độ tuổi phù hợp, mô tả) → Lưu → sửa lại tên.
- **Kết quả mong đợi**: Thêm/sửa thành công, xuất hiện ngay trong danh sách chọn Loại lớp học ở Gói Học.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SET-02 — CRUD Gói Học
- **Vai trò**: Admin
- **Bước thực hiện**: Tab Gói Học → Thêm 1 gói TEST, chọn thuộc Loại lớp học ở trên, nhập thời hạn/số buổi/giá.
- **Kết quả mong đợi**: Thêm thành công, xuất hiện ngay trong danh sách chọn khi tạo Đơn Bán Hàng.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SET-03 — CRUD Ca Học
- **Vai trò**: Admin
- **Bước thực hiện**: Tab Ca Học → Thêm 1 ca TEST với giờ bắt đầu/kết thúc.
- **Kết quả mong đợi**: Thêm thành công, xuất hiện trong danh sách chọn Ca học khi Điểm danh.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SET-04 — CRUD Giáo Viên
- **Vai trò**: Admin
- **Bước thực hiện**: Tab Giáo Viên → Thêm giáo viên TEST, thử **để trống** Hình thức làm việc trước khi Lưu.
- **Kết quả mong đợi**: Hình thức làm việc là bắt buộc — không lưu được nếu để trống; sau khi chọn và lưu, giáo viên xuất hiện ngay trong danh sách Giáo viên phụ trách/Trợ giảng khi Điểm danh.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SET-05 — Ngừng dùng 1 danh mục
- **Vai trò**: Admin
- **Bước thực hiện**: Bấm **Ngừng dùng** trên 1 mục TEST bất kỳ (Loại lớp/Gói học/Ca học/Giáo viên).
- **Kết quả mong đợi**: Hộp thoại xác nhận hiện ra; sau xác nhận, mục đó biến mất khỏi danh sách chọn ở các nghiệp vụ liên quan (không xóa dữ liệu lịch sử).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SET-06 — Kích hoạt lại danh mục đã ngừng dùng
- **Vai trò**: Admin
- **Điều kiện tiên quyết**: Kết quả UAT-SET-05
- **Bước thực hiện**: Bấm **Kích hoạt lại** trên mục vừa ngừng dùng.
- **Kết quả mong đợi**: Mục trở lại danh sách chọn bình thường.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SET-07 — Cấu Hình: bật/tắt "Cho phép học nợ"
- **Vai trò**: Admin
- **Bước thực hiện**: Tab Cấu Hình → bật rồi tắt lại công tắc "Cho phép học nợ".
- **Kết quả mong đợi**: Lưu đúng trạng thái, ảnh hưởng ngay tới hành vi Điểm danh khi hết buổi (xem UAT-DD-09/10).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SET-08 — Cấu Hình: chọn gói học thử
- **Vai trò**: Admin
- **Bước thực hiện**: Tab Cấu Hình → chọn 1 gói học TEST làm "gói học thử".
- **Kết quả mong đợi**: Lưu đúng, công tắc "Buổi học thử" ở popup Điểm danh dùng được ngay (xem UAT-DD-07).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SET-09 — FrontDesk chỉ đọc trên toàn bộ Thiết Lập
- **Vai trò**: FrontDesk
- **Bước thực hiện**: Đăng nhập FrontDesk → vào Admin Center → Thiết Lập → thử Thêm/Sửa/Ngừng dùng ở cả 4 tab danh mục + Cấu Hình.
- **Kết quả mong đợi**: Xem được toàn bộ nội dung (đọc), nhưng **không thực hiện được** thao tác ghi nào — nút bị ẩn/mờ hoặc bị từ chối quyền khi bấm.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-SET-10 — Admin có toàn quyền trên toàn bộ Thiết Lập
- **Vai trò**: Admin
- **Bước thực hiện**: Lặp lại UAT-SET-01 đến 08 bằng tài khoản Admin.
- **Kết quả mong đợi**: Tất cả thao tác Thêm/Sửa/Ngừng dùng/Cấu hình đều thực hiện được.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

---

## UAT-PD — Chứng Từ Đã Ghi Sổ

*(Vào: Chứng Từ Đã Ghi Sổ — xem User Guide mục 8, 9)*

#### UAT-PD-01 — Tra cứu đơn bán đã ghi sổ
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở danh sách Chứng Từ Đã Ghi Sổ → tab Bán Hàng → mở 1 đơn TEST.
- **Kết quả mong đợi**: Xem đúng chi tiết đơn (dòng, tổng tiền, trạng thái thanh toán).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PD-02 — Tra cứu phiếu nhập đã ghi sổ
- **Vai trò**: Cả hai
- **Bước thực hiện**: Tab Nhập Hàng → mở 1 phiếu TEST.
- **Kết quả mong đợi**: Xem đúng chi tiết phiếu.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PD-03 — Đánh dấu đã thu tiền — thu một phần
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Đơn bán TEST còn nợ (chưa thanh toán hết)
- **Bước thực hiện**: Bấm **Đánh dấu đã thu tiền** → nhập số tiền **nhỏ hơn** số còn nợ → Xác nhận.
- **Kết quả mong đợi**: Công nợ học viên giảm đúng số vừa thu; trạng thái thanh toán chuyển "Còn nợ".
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PD-04 — Thu tiền lần 2 đủ số còn lại
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Kết quả UAT-PD-03
- **Bước thực hiện**: Lặp lại Đánh dấu đã thu tiền, nhập đúng số còn nợ lại.
- **Kết quả mong đợi**: Trạng thái thanh toán chuyển "Đã thanh toán", công nợ về 0 cho đơn này.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PD-05 — Đổi trạng thái học
- **Vai trò**: Cả hai
- **Bước thực hiện**: Từ tab Ghi Danh (hồ sơ học viên) hoặc dòng gói học trong đơn bán → bấm **Đổi trạng thái** → chọn "Tạm ngưng" → Xác nhận.
- **Kết quả mong đợi**: Trạng thái đổi thành công, số buổi còn lại không đổi.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PD-06 — Không thể đặt "Hoàn thành" thủ công
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở hộp thoại Đổi trạng thái, xem danh sách trạng thái có thể chọn.
- **Kết quả mong đợi**: Chỉ có Đang học/Tạm ngưng/Đã hủy — **không có** "Hoàn thành" trong danh sách chọn.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PD-07 — Chứng từ đã ghi sổ không cho sửa/xóa dòng
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở 1 đơn bán/phiếu nhập đã ghi sổ, tìm nút Thêm dòng/Sửa dòng/Xóa dòng.
- **Kết quả mong đợi**: Không có nút nào cho phép sửa/xóa/thêm dòng trên chứng từ đã khóa.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PD-08 — FrontDesk vẫn thu tiền/đổi trạng thái được bình thường
- **Vai trò**: FrontDesk
- **Bước thực hiện**: Lặp lại UAT-PD-03 và UAT-PD-05 bằng tài khoản FrontDesk.
- **Kết quả mong đợi**: Cả 2 việc đều thực hiện được — theo ma trận phân quyền, thao tác Thu tiền và Đổi trạng thái học không giới hạn vai trò.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

---

## UAT-LED — Sổ Cái

*(Vào: Chứng Từ Đã Ghi Sổ → Sổ Cái — xem Design §4, trang `entries.tsx`)*

#### UAT-LED-01 — Sổ cái Họa Cụ (Item Ledger)
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở tab Sổ cái Họa Cụ.
- **Kết quả mong đợi**: Hiển thị đúng các bút toán nhập/xuất kho đã phát sinh (khớp với các phiếu nhập/đơn bán đã ghi sổ ở trên).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-LED-02 — Bút toán giá trị (Value Ledger)
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở tab Bút Toán Giá Trị.
- **Kết quả mong đợi**: Hiển thị đúng giá vốn/doanh thu tương ứng các giao dịch họa cụ.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-LED-03 — Sổ Buổi Học toàn cục (Session Ledger)
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở tab Sổ Buổi Học (nhiều học viên cùng lúc, không chỉ 1 học viên như ở hồ sơ học viên).
- **Kết quả mong đợi**: Hiển thị đúng toàn bộ bút toán buổi học của mọi học viên; có nút **Chi tiết** trên mỗi dòng, và nút **Hủy điểm danh** xuất hiện trong popup chi tiết cho dòng loại "Điểm Danh" chưa bị hủy.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-LED-04 — Sổ Công Nợ Học Viên (Student Ledger)
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở tab Sổ Công Nợ.
- **Kết quả mong đợi**: Hiển thị đúng các bút toán ghi nợ/thu tiền/hoàn tiền.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-LED-05 — Sổ Nhân Viên (Employee Ledger)
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở tab Sổ Nhân Viên.
- **Kết quả mong đợi**: Hiển thị đúng bút toán lương theo từng giáo viên, khớp các bảng lương đã ghi sổ.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-LED-06 — Sổ Tiền Mặt (Cash Ledger)
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở tab Sổ Tiền Mặt.
- **Kết quả mong đợi**: Hiển thị đúng mọi bút toán thu/chi tổng hợp, khớp với trang Dòng Tiền Mặt.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-LED-07 — Đối Soát (Reconcile) bởi Admin
- **Vai trò**: Admin
- **Bước thực hiện**: Bấm nút **Đối Soát** → chọn phạm vi (ví dụ "Họa cụ") → xác nhận.
- **Kết quả mong đợi**: Thực hiện thành công, số liệu cache (tồn kho/buổi còn lại/công nợ tùy phạm vi) được tính lại khớp đúng tổng sổ cái.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-LED-08 — FrontDesk bị từ chối quyền Đối Soát
- **Vai trò**: FrontDesk
- **Bước thực hiện**: Đăng nhập FrontDesk → tìm/bấm nút Đối Soát.
- **Kết quả mong đợi**: Thấy nút nhưng khi bấm nhận **thông báo không đủ quyền rõ ràng** (không phải lỗi kỹ thuật khó hiểu kiểu mã lỗi HTTP).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-LED-09 — Không ai sửa/xóa trực tiếp Sổ Cái/Chứng Từ Đã Ghi Sổ
- **Vai trò**: Admin
- **Bước thực hiện**: Rà soát toàn bộ 6 tab Sổ Cái + trang Chứng Từ Đã Ghi Sổ, kể cả bằng tài khoản Admin.
- **Kết quả mong đợi**: Không có bất kỳ nút Tạo/Sửa/Xóa trực tiếp nào — mọi thay đổi chỉ qua các nghiệp vụ điều chỉnh được thiết kế riêng (Thu tiền, Đổi trạng thái học, Hủy điểm danh, Đảo ngược ghi sổ, Đối Soát).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

---

## UAT-STAT — Thống Kê

*(Vào: Tổng Quan → Thống Kê — xem User Guide mục 10)*

#### UAT-STAT-01 — Doanh thu theo tháng tách Khóa học/Họa cụ
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở trang Thống Kê.
- **Kết quả mong đợi**: Biểu đồ/bảng doanh thu theo tháng, tách riêng phần Khóa học và Họa cụ, khớp với các chứng từ đã ghi sổ.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-STAT-02 — Phân bổ đăng ký theo loại lớp học
- **Vai trò**: Cả hai
- **Bước thực hiện**: Quan sát biểu đồ phân bổ theo Loại lớp học.
- **Kết quả mong đợi**: Số liệu khớp với số lượt đăng ký thực tế đang hoạt động theo từng loại lớp.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-STAT-03 — Danh sách học viên sắp hết buổi (≤ 3 buổi)
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Có ít nhất 1 học viên TEST còn ≤ 3 buổi
- **Bước thực hiện**: Xem danh sách "sắp hết buổi".
- **Kết quả mong đợi**: Học viên đó xuất hiện đúng trong danh sách; học viên còn nhiều buổi không xuất hiện.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-STAT-04 — Danh sách công nợ chưa thu
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Có ít nhất 1 học viên TEST còn công nợ
- **Bước thực hiện**: Xem danh sách công nợ chưa thu.
- **Kết quả mong đợi**: Hiển thị đúng học viên và đúng số tiền còn nợ.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

---

## UAT-RC — Role Center / Bảng Điều Khiển

*(Vào: Tổng Quan → Role Center — xem User Guide mục 10)*

#### UAT-RC-01 — KPI hôm nay
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở trang Role Center (trang mặc định sau đăng nhập).
- **Kết quả mong đợi**: Hiển thị đúng 4 KPI: số đăng ký đang hoạt động, doanh thu tháng này, số buổi học hôm nay, số lượt sắp hết buổi.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-RC-02 — Danh sách chứng từ cần xử lý
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Có ít nhất 1 đơn bán/phiếu nhập TEST **chưa ghi sổ**
- **Bước thực hiện**: Xem danh sách "Chứng từ cần xử lý".
- **Kết quả mong đợi**: Đơn/phiếu nháp đó xuất hiện đúng trong danh sách.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-RC-03 — Điều hướng từ Role Center tới chứng từ
- **Vai trò**: Cả hai
- **Bước thực hiện**: Bấm vào 1 dòng trong danh sách chứng từ cần xử lý.
- **Kết quả mong đợi**: Điều hướng đúng tới đúng đơn/phiếu đó để tiếp tục xử lý.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

---

## UAT-PERM — Phân quyền, bất biến chứng từ & an toàn thao tác

*(Tham chiếu ma trận phân quyền Design §5 và các quy tắc an toàn Design §6)*

#### UAT-PERM-01 — Bảng tổng hợp kiểm tra phân quyền theo từng hành động giới hạn
- **Vai trò**: Cả hai (chạy lần lượt)
- **Bước thực hiện**: Với từng hành động dưới đây, thử bằng cả 2 tài khoản và điền kết quả:

  | Hành động | Admin phải làm được | FrontDesk phải bị chặn |
  |---|---|---|
  | Đối Soát (Reconcile) | ☐ | ☐ |
  | Đảo ngược Đơn Bán Hàng | ☐ | ☐ |
  | Đảo ngược Phiếu Nhập Họa Cụ | ☐ | ☐ |
  | Hủy điểm danh của ngày **không phải** hôm nay | ☐ | ☐ |
  | Thêm/Sửa/Ngừng dùng danh mục (Loại lớp/Gói học/Ca học/Giáo viên) | ☐ | ☐ |
  | Sửa Cấu Hình chung | ☐ | ☐ |

- **Kết quả mong đợi**: Admin làm được **tất cả**; FrontDesk bị chặn **tất cả** — và khi bị chặn, thông báo phải là lỗi nghiệp vụ rõ ràng (ví dụ "không đủ quyền thực hiện"), **không phải** một lỗi kỹ thuật khó hiểu (ví dụ mã lỗi HTTP 403 hiển thị nguyên văn cho người dùng — đây từng là một lỗi thật đã được phát hiện và sửa, xem ghi chú vận hành nội bộ).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PERM-02 — Double-click "Ghi sổ" không tạo dữ liệu trùng
- **Vai trò**: Cả hai
- **Bước thực hiện**: Trên 1 đơn bán TEST đã điền đủ dòng, bấm **Ghi sổ đơn hàng** → xác nhận → ngay sau khi hộp thoại đóng, thử bấm ghi sổ lại lần nữa trên cùng đơn (nếu nút còn hiển thị được).
- **Kết quả mong đợi**: Chỉ có **đúng 1** lượt đăng ký/bút toán được tạo ra — lần bấm thứ 2 hoặc bị chặn nút, hoặc báo đơn đã ở trạng thái Posted, không tạo thêm bản ghi trùng.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PERM-03 — Double-click Điểm danh không trừ buổi 2 lần
- **Vai trò**: Cả hai
- **Bước thực hiện**: Điểm danh 1 học viên TEST với gói/ngày/ca cụ thể → ngay sau khi thấy thông báo thành công, mở lại popup Điểm danh và lặp lại **y hệt** gói/ngày/ca đó.
- **Kết quả mong đợi**: Lần 2 nhận thông báo **"Hệ thống đã bỏ qua yêu cầu này..."**, số buổi còn lại không đổi so với sau lần 1 (xem chi tiết UAT-DD-06).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PERM-04 — Dialog xác nhận trước mọi hành động ghi sổ
- **Vai trò**: Cả hai
- **Bước thực hiện**: Với cả 3 loại chứng từ (Đơn Bán Hàng, Phiếu Nhập Họa Cụ, Bảng Lương): điền đủ thông tin hợp lệ, bấm nút ghi sổ, sau đó bấm **Hủy/Đóng** trên hộp thoại xác nhận (không xác nhận thật).
- **Kết quả mong đợi**: Chứng từ **vẫn ở trạng thái nháp**, chưa bị ghi sổ, có thể sửa tiếp bình thường.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PERM-05 — Dialog xác nhận trước khi Ngừng dùng
- **Vai trò**: Cả hai
- **Bước thực hiện**: Bấm Ngừng hoạt động/Ngừng dùng trên 1 học viên/họa cụ/giáo viên/danh mục TEST bất kỳ, sau đó bấm Hủy trên hộp thoại xác nhận.
- **Kết quả mong đợi**: Bản ghi **vẫn hoạt động bình thường**, không bị ngừng dùng.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PERM-06 — Lazy-load 50 dòng khi cuộn trang
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Trang có > 50 bản ghi (ví dụ Hồ Sơ Học Viên nếu đã có sẵn nhiều dữ liệu, hoặc Sổ Cái)
- **Bước thực hiện**: Mở danh sách, đếm số dòng hiển thị ban đầu → cuộn xuống gần cuối danh sách.
- **Kết quả mong đợi**: Ban đầu chỉ hiển thị 50 dòng; khi cuộn gần cuối, tự động tải thêm 50 dòng tiếp theo kèm chỉ báo "Đang tải thêm..." — không cần bấm nút nào.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PERM-07 — Nút "Làm mới" và nhãn thời gian cập nhật
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở 1 trang danh sách bất kỳ, đợi vài phút, quan sát nhãn "Cập nhật ... trước" → bấm **Làm mới**.
- **Kết quả mong đợi**: Trước khi bấm, nhãn hiển thị đúng thời gian đã trôi qua (ví dụ "3 phút trước"); sau khi bấm Làm mới, nhãn đổi thành "vừa xong" và dữ liệu được tải lại.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PERM-08 — Chứng Từ Đã Ghi Sổ/Sổ Cái bất biến qua các nghiệp vụ điều chỉnh
- **Vai trò**: Admin
- **Bước thực hiện**: Thực hiện 1 vòng đầy đủ: ghi sổ đơn bán → thu tiền 1 phần → đổi trạng thái học → hủy 1 điểm danh liên quan → đảo ngược ghi sổ đơn đó (nếu đủ điều kiện). Sau mỗi bước, kiểm tra lại bản ghi Đã Ghi Sổ/Sổ Cái gốc.
- **Kết quả mong đợi**: Không bước nào **sửa hoặc xóa** bản ghi gốc — mỗi bước chỉ **thêm bút toán/bản ghi mới** (bù trừ/điều chỉnh) và cập nhật cờ trạng thái (ví dụ "Đã bị hủy", "Đã đảo ngược") trên bản ghi gốc.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PERM-09 — Bản ghi gốc còn nguyên sau Đảo ngược ghi sổ
- **Vai trò**: Admin
- **Điều kiện tiên quyết**: Kết quả UAT-SO-12 hoặc UAT-PC-07
- **Bước thực hiện**: Tìm lại đúng đơn/phiếu Đã Ghi Sổ gốc vừa đảo ngược trong Chứng Từ Đã Ghi Sổ.
- **Kết quả mong đợi**: Bản ghi gốc **vẫn còn**, đầy đủ dữ liệu cũ, chỉ thêm nhãn "Đã đảo ngược" — không bị xóa khỏi hệ thống.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PERM-10 — Bản ghi gốc còn nguyên sau Hủy điểm danh
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Kết quả UAT-DD-13
- **Bước thực hiện**: Tìm lại đúng dòng điểm danh gốc vừa hủy trong Sổ Buổi Học.
- **Kết quả mong đợi**: Dòng gốc **vẫn còn** trong lịch sử, chỉ chuyển nhãn "Đã bị hủy" — không biến mất khỏi danh sách.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

---

## Sau khi hoàn tất UAT

- Tổng hợp toàn bộ test case "Không đạt" thành danh sách lỗi (bug list) riêng, kèm ảnh chụp
  màn hình và bước tái hiện, gửi lại đội kỹ thuật.
- Dọn dẹp toàn bộ dữ liệu TEST đã tạo trong quá trình UAT (học viên/giáo viên/gói học/chứng
  từ có tên "TEST") trước khi hệ thống đi vào vận hành thật — nhờ đội kỹ thuật hỗ trợ nếu cần
  xóa dữ liệu đã ghi sổ.
- Chỉ coi hệ thống **sẵn sàng nghiệm thu** khi toàn bộ test case nhóm `UAT-PERM` (phân quyền
  và bất biến chứng từ) đạt — đây là các nguyên tắc nền tảng không được phép sai lệch.
