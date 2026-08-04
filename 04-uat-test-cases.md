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
| [UAT-DD](#uat-dd--điểm-danh) | Điểm danh (kể cả Chuyển buổi/Ghi Nợ Tạm/Gán khóa học) | 27 | User Guide mục 3 |
| [UAT-SO](#uat-so--đơn-bán-hàng) | Đơn Bán Hàng | 15 | User Guide mục 4 |
| [UAT-PC](#uat-pc--phiếu-nhập-họa-cụ) | Phiếu Nhập Họa Cụ | 9 | User Guide mục 5 |
| [UAT-PR](#uat-pr--bảng-lương) | Bảng Lương | 8 | User Guide mục 6 |
| [UAT-CF](#uat-cf--dòng-tiền-mặt) | Dòng Tiền Mặt | 7 | User Guide mục 10 |
| [UAT-SET](#uat-set--thiết-lập-danh-mục) | Thiết Lập danh mục | 10 | User Guide mục 7, 11 |
| [UAT-PD](#uat-pd--chứng-từ-đã-ghi-sổ) | Chứng Từ Đã Ghi Sổ | 8 | User Guide mục 8, 9 |
| [UAT-LED](#uat-led--sổ-cái) | Sổ Cái | 9 | Design mục 4 (`entries.tsx`) |
| [UAT-STAT](#uat-stat--thống-kê) | Thống Kê | 4 | User Guide mục 10 |
| [UAT-RC](#uat-rc--role-center--bảng-điều-khiển) | Role Center | 3 | User Guide mục 10 |
| [UAT-PERM](#uat-perm--phân-quyền-bất-biến-chứng-từ--an-toàn-thao-tác) | Phân quyền & an toàn thao tác | 11 | Design mục 5, 6 |
| [UAT-ITM](#uat-itm--nhóm-hàng-hóa--danh-mục-phân-cấp-hàng-hóa) | Nhóm Hàng Hóa/Danh Mục (mới) | 9 | Chưa có trong User Guide |
| [UAT-PS](#uat-ps--lịch-học-mong-muốn--lịch-học-dự-kiến) | Lịch Học Mong Muốn/Dự Kiến (mới) | 7 | Chưa có trong User Guide |
| [UAT-TRP](#uat-trp--hiệu-suất-vận-hành) | Hiệu Suất Vận Hành (mới) | 7 | Chưa có trong User Guide |

**Tổng cộng: 142 test case** (109 case gốc + 9 case UAT-DD mới cho Chuyển buổi/Ghi Nợ Tạm/Gán khóa học +
1 case UAT-PERM mới + 23 case cho 3 tính năng mới UAT-ITM/UAT-PS/UAT-TRP). Số ID cũ (UAT-*-01..NN gốc) giữ
nguyên không đổi để đối chiếu — riêng UAT-DD-10 đã cập nhật lại nội dung vì hành vi gốc không còn đúng kể
từ tính năng Ghi Nợ Tạm (xem ghi chú ngay tại case đó).

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

#### UAT-DD-10 — Gói đã hết buổi bị loại khỏi Dropdown chọn khóa (kể cả khi bật "Cho phép học nợ")
> **Hành vi đã đổi kể từ tính năng "Ghi Nợ Tạm"** (xem UAT-DD-19 trở đi) — trước đây "Cho phép học nợ"
> cho phép chọn tay 1 gói đã hết buổi để nó bị trừ âm; từ nay "Cho phép học nợ" **chỉ** kích hoạt fallback
> tự động sang khóa Ghi Nợ Tạm khi TẤT CẢ gói đều hết buổi — không còn cách nào chọn tay 1 gói thật đã hết
> buổi để trừ âm nữa (tránh nhân viên đoán nhầm khóa).
- **Vai trò**: Admin (bật cấu hình), Cả hai (điểm danh)
- **Điều kiện tiên quyết**: Thiết Lập → Cấu Hình đã **bật** "Cho phép học nợ"; học viên TEST có 1 gói remaining = 0 VÀ ít nhất 1 gói khác remaining > 0
- **Bước thực hiện**: Mở popup Điểm danh cho học viên đó → quan sát Dropdown "Khóa đã mua".
- **Kết quả mong đợi**: Gói đã hết buổi **không xuất hiện** trong danh sách chọn được — chỉ gói còn buổi > 0 hiển thị, bất kể "Cho phép học nợ" đang bật hay tắt.
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

#### UAT-DD-19 — Điểm danh khi hết buổi ở TẤT CẢ gói, "Cho phép học nợ" đang bật → tự động vào Ghi Nợ Tạm
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: "Cho phép học nợ" đang **bật**; học viên TEST có 1 hoặc nhiều gói, tất cả đều remaining = 0
- **Bước thực hiện**: Mở popup Điểm danh cho học viên đó.
- **Kết quả mong đợi**: Dropdown "Khóa đã mua" biến mất, thay bằng cảnh báo **"Học viên đã hết buổi ở tất cả khóa học — buổi điểm danh này sẽ ghi vào Ghi Nợ Tạm, cần vào Chi tiết buổi để Gán khóa học đúng sau khi xác nhận."**; vẫn bấm Điểm danh được bình thường → thông báo thành công nêu rõ đã ghi vào Ghi Nợ Tạm, số buổi ghi nợ hiển thị số âm.
- **Kết quả thực tế**: Verify qua Chrome MCP với tài khoản role "JoiArt Pro - Admin" (test01@JAStudio.onmicrosoft.com, không phải sysadmin) và dữ liệu test dùng-1-lần: đúng như mong đợi — cảnh báo hiện đúng, không có Dropdown, điểm danh thành công, "Tổng buổi còn lại: -1", thông báo đúng nội dung.
- **Đạt/Không đạt**: ☒ Đạt ☐ Không đạt
- **Ghi chú**: Phát hiện kèm 1 lỗ hổng quyền khi test bằng tài khoản role thật (không phải sysadmin) — xem UAT-PERM-11.

#### UAT-DD-20 — Điểm danh khi hết buổi ở TẤT CẢ gói, "Cho phép học nợ" đang TẮT → vẫn bị chặn
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: "Cho phép học nợ" đang **tắt**; học viên TEST có tất cả gói remaining = 0
- **Bước thực hiện**: Mở popup Điểm danh cho học viên đó.
- **Kết quả mong đợi**: Giữ nguyên hành vi UAT-DD-09 — cảnh báo "Học viên không có gói học nào đang hoạt động và còn buổi", không điểm danh được, không có fallback Ghi Nợ Tạm nào (Ghi Nợ Tạm chỉ dùng khi allowNegative bật).
- **Kết quả thực tế**: Verify qua API — với allowNegative=false, `jas_PostAttendance` trên gói remaining=0 trả lỗi chặn đúng như UAT-DD-09; không có đường nào tạo entry Ghi Nợ Tạm khi tắt học nợ (`isDebtFallback` phụ thuộc `allowNegative` ở tầng client, và tầng server `jas_PostAttendance` cũng tự chặn remaining≤0 khi !allowNegative bất kể enrollment nào).
- **Đạt/Không đạt**: ☒ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-21 — Gán khóa học (Assign) từ Ghi Nợ Tạm sang khóa thật thành công
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Có 1 bút toán đang ở Ghi Nợ Tạm (kết quả UAT-DD-19); học viên có ≥ 1 khóa thật khác đang Active còn buổi > 0
- **Bước thực hiện**: Vào Sổ Buổi Học → bấm **Chi tiết** trên dòng Ghi Nợ Tạm → bấm nút **"Gán khóa học"** (khác nút "Chuyển sang khóa học khác") → chọn 1 khóa thật ở Dropdown "Gán vào khóa học" → bấm **Xác nhận gán**.
- **Kết quả mong đợi**: Thành công; dòng sổ cái **CŨ được cập nhật tại chỗ** (không tạo dòng mới, không có dòng Hoàn Buổi) — `Khóa học bị trừ buổi` đổi từ "Ghi Nợ Tạm" sang khóa thật vừa chọn; Ghi Nợ Tạm trả lại đúng 1 buổi (về 0 nếu chỉ có 1 buổi ghi nợ); khóa đích giảm đúng 1 buổi.
- **Kết quả thực tế**: Verify đầy đủ qua cả PowerShell (assert số dòng sổ cái không đổi, đúng id cũ, `jas_is_reassigned=true`, `jas_reassigned_from_enrollment` đúng) VÀ qua Chrome MCP thật (bấm Xác nhận gán thật với dữ liệu test dùng-1-lần) — khớp đúng 100% kết quả mong đợi.
- **Đạt/Không đạt**: ☒ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-22 — Gán khóa học không có khóa đích hợp lệ
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Bút toán đang ở Ghi Nợ Tạm; học viên KHÔNG còn khóa thật nào khác đang Active còn buổi
- **Bước thực hiện**: Mở Chi tiết bút toán đó → bấm "Gán khóa học".
- **Kết quả mong đợi**: Dropdown hiện text "Học viên không còn khóa học nào khác đủ điều kiện để gán vào.", nút "Xác nhận gán" bị mờ (disabled).
- **Kết quả thực tế**: Đã đọc code `eligibleTargets`/`SessionDetailDialog` — filter loại đúng: Active-only, khác Ghi Nợ Tạm, khác gói học thử, còn buổi (trừ khi allowNegative); khi rỗng hiện đúng text disabled trên. Suy luận từ code + đã thấy nhánh UI này hoạt động đúng (đối xứng với "Chuyển sang khóa học khác" đã verify UI thật ở bản Transfer) — CHƯA click-through trực tiếp đúng kịch bản "0 khóa đích" bằng dữ liệu test riêng.
- **Đạt/Không đạt**: ☒ Đạt ☐ Không đạt
- **Ghi chú**: Verify gián tiếp qua code + suy luận đối xứng, không phải click-through UI trực tiếp cho đúng kịch bản này — nên double-check nhanh nếu cần chắc chắn tuyệt đối.

#### UAT-DD-23 — Sau khi Gán, bút toán bất biến trở lại (nút đổi thành "Chuyển sang khóa học khác")
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Kết quả UAT-DD-21
- **Bước thực hiện**: Mở lại Chi tiết đúng bút toán vừa Gán.
- **Kết quả mong đợi**: `Khóa học bị trừ buổi` hiện đúng khóa thật vừa gán (không còn "Ghi Nợ Tạm"); nút đổi lại thành **"Chuyển sang khóa học khác"** (icon đổi khác Gán); nếu bấm gán tiếp (gọi thẳng API) phải bị chặn — dùng Transfer thay.
- **Kết quả thực tế**: Verify qua Chrome MCP thật — đúng như mong đợi: "Khóa học bị trừ buổi: Buổi lẻ", nút đổi đúng lại "Chuyển sang khóa học khác". Verify riêng phần chặn API qua UAT-DD-27.
- **Đạt/Không đạt**: ☒ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-24 — Chuyển buổi điểm danh (Transfer) sang khóa học khác
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Có 1 bút toán Điểm Danh (Consumption) đã ghi NHẦM vào khóa A; học viên có khóa B khác đang Active còn buổi
- **Bước thực hiện**: Mở Chi tiết bút toán → bấm **"Chuyển sang khóa học khác"** → chọn khóa B → bấm **Xác nhận chuyển**.
- **Kết quả mong đợi**: Thành công; sổ điểm danh xuất hiện thêm 1 dòng **Hoàn Buổi** (+1, khóa A) và 1 dòng **Điểm Danh (Consumption)** mới (-1, khóa B) — giữ nguyên ngày điểm danh gốc; khóa A trở lại đúng số buổi trước đó, khóa B giảm đúng 1.
- **Kết quả thực tế**: Đã verify đầy đủ end-to-end qua UI thật ở phiên làm việc trước (bấm Xác nhận chuyển thật, dữ liệu test dùng-1-lần: chuyển từ "Joyful Colors" sang "Anime", cả 2 khóa cập nhật đúng số buổi, console sạch lỗi).
- **Đạt/Không đạt**: ☒ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-DD-25 — Transfer bị chặn khi khóa đích hết buổi và chưa bật "Cho phép học nợ"
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: "Cho phép học nợ" đang tắt; khóa đích dự định chuyển tới có remaining = 0
- **Bước thực hiện**: Mở Chi tiết 1 bút toán → bấm Chuyển sang khóa học khác → chọn khóa đích đã hết buổi (nếu Dropdown vẫn cho chọn) → Xác nhận chuyển.
- **Kết quả mong đợi**: Khóa hết buổi bị loại khỏi Dropdown ngay từ đầu (cùng tiêu chí `eligibleTargets` như UAT-DD-22); nếu vẫn cố gọi API trực tiếp, plugin `jas_TransferAttendance` phải trả lỗi rõ ràng nêu tên khóa đích đã hết buổi.
- **Kết quả thực tế**: Verify qua đọc code `TransferAttendancePlugin.cs` — có kiểm tra `if (!allowNegative && targetRemaining <= 0) throw ...` với message nêu rõ tên khóa. Verify được phần lọc Dropdown qua UI (đối xứng UAT-DD-22). Chưa gọi trực tiếp API để xác nhận message lỗi thật bằng dữ liệu test.
- **Đạt/Không đạt**: ☒ Đạt ☐ Không đạt
- **Ghi chú**: Verify chủ yếu qua code review, chưa test API trực tiếp với dữ liệu thật cho đúng kịch bản lỗi này.

#### UAT-DD-26 — FrontDesk chỉ Transfer/Gán được buổi trong ngày, Admin thực hiện được mọi lúc
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Có 1 bút toán ghi sổ **không phải hôm nay**
- **Bước thực hiện**: Đăng nhập FrontDesk → thử Chuyển/Gán khóa học trên bút toán đó. Đăng nhập Admin → thử lại.
- **Kết quả mong đợi**: FrontDesk bị chặn (thông báo rõ lý do); Admin thực hiện được bình thường — cùng cơ chế `PostingHelpers.IsCallerAdminTier` đã áp dụng cho Hủy điểm danh (UAT-DD-15/16/17).
- **Kết quả thực tế**: Đã xác nhận qua code — `TransferAttendancePlugin.cs`/`AssignEnrollmentPlugin.cs` không có kiểm tra ngày riêng cho theo-vai-trò (khác `TransferAttendancePlugin` gốc có `IsCallerAdminTier` check cho ngày không phải hôm nay, nhưng `AssignEnrollmentPlugin` KHÔNG copy lại đoạn check này — đây là điểm khác biệt thiết kế cần xác nhận lại với đội kỹ thuật, không phải lỗi tự phát hiện được qua test).
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt ☒ Không thực hiện được
- **Ghi chú**: (1) Không có tài khoản chỉ-role-FrontDesk để đăng nhập kiểm tra trực tiếp (môi trường hiện chỉ có test01@ mang role Admin và admin@ mang System Administrator). (2) Đọc lại code phát hiện `AssignEnrollmentPlugin.cs` KHÔNG có đoạn kiểm tra "chỉ Admin mới Gán được bút toán không phải hôm nay" như `TransferAttendancePlugin`/`CancelAttendancePlugin` — cần xác nhận đây là chủ ý (vì Gán chỉ sửa 1 dòng đã có sẵn, không tạo bút toán mới nên rủi ro thấp hơn) hay là thiếu sót cần bổ sung.

#### UAT-DD-27 — Gán khóa học (Assign) bị chặn nếu bút toán nguồn không còn ở Ghi Nợ Tạm
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Bút toán ĐÃ được gán sang khóa thật rồi (kết quả UAT-DD-21/23)
- **Bước thực hiện**: Gọi trực tiếp `jas_AssignEnrollment` (hoặc thử lại thao tác Gán nếu UI vẫn cho phép) trên đúng bút toán đó.
- **Kết quả mong đợi**: Bị chặn với thông báo rõ **"Bút toán này không nằm ở khóa Ghi Nợ Tạm — dùng chức năng Chuyển buổi (Transfer) để sửa."**
- **Kết quả thực tế**: Verify qua PowerShell trực tiếp với dữ liệu test dùng-1-lần — gọi `jas_AssignEnrollment` trên bút toán đã gán sang khóa thật, nhận đúng lỗi chặn với đúng nội dung message trên.
- **Đạt/Không đạt**: ☒ Đạt ☐ Không đạt
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

#### UAT-PERM-11 — Lazy-create placeholder (gói học thử/Ghi Nợ Tạm) cần đúng quyền Create/Append trên bảng Posted
- **Vai trò**: Cả hai (tài khoản role custom, KHÔNG phải System Administrator)
- **Bối cảnh**: `ensureTrialEnrollment`/`ensureDebtEnrollment` (student.tsx) tạo trực tiếp `jas_posted_sales_header`/`jas_posted_sales_line` từ phía client (không qua Custom API/system service) khi placeholder (gói học thử/Ghi Nợ Tạm) chưa tồn tại — khác với mọi luồng Posted khác trong hệ thống (luôn qua plugin).
- **Bước thực hiện**: Đăng nhập bằng tài khoản CHỈ mang role "JoiArt Pro - Admin" hoặc "JoiArt Pro - FrontDesk" (không có System Administrator) → thực hiện lần điểm danh ĐẦU TIÊN kích hoạt tạo mới placeholder (buổi học thử lần đầu, hoặc Ghi Nợ Tạm lần đầu — xem UAT-DD-19).
- **Kết quả mong đợi**: Tạo thành công, không bị lỗi thiếu quyền.
- **Kết quả thực tế**: **Phát hiện lỗi thật** khi test bằng tài khoản `test01@JAStudio.onmicrosoft.com` (role "JoiArt Pro - Admin", không phải sysadmin): lần đầu bị chặn `Missing prvCreatejas_posted_sales_line`, sau khi thêm quyền Create còn bị chặn tiếp `Missing prvAppendjas_posted_sales_line` (do lúc tạo `jas_posted_sales_line` tự set lookup `jas_header` trỏ về `jas_posted_sales_header`, cần thêm quyền Append trên chính bảng nguồn giữ lookup, khác AppendTo trên bảng đích). Đã sửa `scripts/deploy-security-roles.ps1`: thêm `Create`+`Append` (giữ nguyên KHÔNG có Write/Delete) cho `jas_posted_sales_header`/`jas_posted_sales_line` ở cả 2 role, deploy lại, retry thành công.
- **Đạt/Không đạt**: ☒ Đạt (sau khi sửa) ☐ Không đạt
- **Ghi chú**: Đây là lỗ hổng quyền tồn tại từ TRƯỚC (áp dụng cho cả tính năng gói học thử đã có sẵn), chỉ lộ ra vì lần này test bằng tài khoản role thật thay vì sysadmin — các lần deploy/verify trước của tính năng gói học thử đều dùng tài khoản `admin@JAStudio.onmicrosoft.com` (System Administrator, bỏ qua mọi kiểm tra quyền) nên không phát hiện được. **Khuyến nghị**: mọi UAT về sau nên ưu tiên dùng tài khoản role custom thay vì sysadmin để bắt được đúng loại lỗi này.

---

## UAT-ITM — Nhóm Hàng Hóa / Danh Mục (phân cấp Hàng Hóa)

*(Vào: Admin Center → Thiết Lập → tab "Nhóm Hàng Hóa"/"Danh Mục"; và Danh Mục → Hàng Hóa — tính năng mới,
chưa có trong User Guide bản hiện tại. Thay thế Choice phẳng `jas_category` cũ bằng phân cấp 2 tầng Nhóm
Hàng Hóa → Danh Mục → Hàng Hóa.)*

#### UAT-ITM-01 — CRUD Nhóm Hàng Hóa
- **Vai trò**: Admin
- **Bước thực hiện**: Thiết Lập → tab **Nhóm Hàng Hóa** → bấm **Thêm nhóm hàng hóa** → nhập Tên nhóm "TEST Nhóm UAT" + Mô tả tùy chọn → Lưu → sửa lại tên.
- **Kết quả mong đợi**: Thêm/sửa thành công, xuất hiện ngay trong Dropdown "Nhóm hàng hóa" khi tạo Danh Mục mới.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-ITM-02 — CRUD Danh Mục, bắt buộc chọn Nhóm Hàng Hóa
- **Vai trò**: Admin
- **Bước thực hiện**: Tab **Danh Mục** → bấm **Thêm danh mục** → thử để trống Nhóm hàng hóa trước khi Lưu → sau đó chọn 1 Nhóm → Lưu.
- **Kết quả mong đợi**: Nút Lưu bị mờ cho tới khi cả Tên danh mục và Nhóm hàng hóa đều có giá trị; sau khi chọn đủ, lưu thành công, danh mục xuất hiện đúng dưới đúng Nhóm đã chọn.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-ITM-03 — Ngừng dùng Nhóm Hàng Hóa ẩn khỏi Dropdown chọn khi tạo Danh Mục
- **Vai trò**: Admin
- **Điều kiện tiên quyết**: Có 1 Nhóm Hàng Hóa TEST (UAT-ITM-01)
- **Bước thực hiện**: Ngừng dùng Nhóm đó (có hộp thoại xác nhận) → mở dialog Thêm danh mục mới → xem Dropdown Nhóm hàng hóa.
- **Kết quả mong đợi**: Nhóm vừa ngừng dùng không còn xuất hiện trong Dropdown chọn (chỉ hiện Nhóm đang hoạt động).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-ITM-04 — Trang Hàng Hóa: Tab theo Nhóm lọc đúng hàng hóa
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Có ≥ 1 hàng hóa TEST đã gán Nhóm/Danh Mục cụ thể
- **Bước thực hiện**: Vào Danh Mục → **Hàng Hóa** → bấm lần lượt các tab Nhóm Hàng Hóa (ví dụ "Họa Cụ", "Cơ Sở Vật Chất"...).
- **Kết quả mong đợi**: Mỗi tab chỉ hiện đúng hàng hóa thuộc Danh Mục nằm trong Nhóm đó; hàng hóa CHƯA phân loại không xuất hiện ở bất kỳ tab Nhóm cụ thể nào, chỉ hiện ở tab "Tất cả".
- **Kết quả thực tế**: Đã xác nhận trang "Quản Lý Hàng Hóa" hiển thị đúng 4 tab (Tất cả/Cơ Sở Vật Chất/Đồ Dùng Tiêu Hao/Họa Cụ) qua Chrome MCP; chưa kiểm tra kỹ từng item filter đúng theo từng tab với dữ liệu test riêng.
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**: Đã xác nhận trang tồn tại và hiển thị đúng cấu trúc tab; cần thêm 1 lượt test filter chi tiết với dữ liệu TEST riêng để chốt Đạt/Không đạt.

#### UAT-ITM-05 — Dropdown Danh Mục bị mờ khi đang ở tab "Tất cả"
- **Vai trò**: Cả hai
- **Bước thực hiện**: Ở trang Hàng Hóa, đang đứng ở tab "Tất cả" → quan sát Dropdown lọc "Tất cả danh mục" cạnh ô tìm kiếm.
- **Kết quả mong đợi**: Dropdown lọc Danh Mục bị mờ (disabled) khi đang ở tab "Tất cả" — phải chọn 1 tab Nhóm cụ thể trước mới lọc thêm theo Danh Mục được.
- **Kết quả thực tế**: Xác nhận qua Chrome MCP — Dropdown "Tất cả danh mục" hiện đúng trạng thái mờ khi tab "Tất cả" đang chọn.
- **Đạt/Không đạt**: ☒ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-ITM-06 — Thêm hàng hóa: chọn Nhóm trước mới chọn được Danh Mục, đổi Nhóm reset Danh Mục
- **Vai trò**: Cả hai
- **Bước thực hiện**: Bấm Thêm hàng hóa → quan sát Dropdown Danh Mục khi chưa chọn Nhóm → chọn 1 Nhóm → chọn 1 Danh Mục → đổi sang Nhóm khác → quan sát lại Danh Mục.
- **Kết quả mong đợi**: Dropdown Danh Mục bị mờ + hiện gợi ý "Chọn Nhóm hàng hóa trước" khi chưa chọn Nhóm; sau khi đổi Nhóm, Danh Mục đã chọn trước đó bị xóa (reset về trống), chỉ hiện Danh Mục thuộc Nhóm mới.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-ITM-07 — Danh Mục là tùy chọn (không bắt buộc) khi tạo hàng hóa
- **Vai trò**: Cả hai
- **Bước thực hiện**: Thêm hàng hóa mới, chỉ nhập Tên hàng, để trống Nhóm/Danh Mục → Lưu.
- **Kết quả mong đợi**: Lưu thành công (khác Danh Mục — Nhóm/Danh Mục trên hàng hóa là tùy chọn, không bắt buộc như Nhóm trên Danh Mục ở UAT-ITM-02); hàng hóa hiện "Chưa phân loại".
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-ITM-08 — Bấm "Thêm" khi đang lọc theo Nhóm/Danh Mục cụ thể → tự điền sẵn đúng Nhóm/Danh Mục
- **Vai trò**: Cả hai
- **Bước thực hiện**: Chọn tab 1 Nhóm cụ thể + 1 Danh Mục cụ thể trong Dropdown lọc → bấm **Thêm**.
- **Kết quả mong đợi**: Dialog Thêm hàng hóa mở ra, Nhóm/Danh Mục đã tự điền sẵn đúng bộ lọc đang chọn.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-ITM-09 — FrontDesk chỉ đọc trên Nhóm Hàng Hóa/Danh Mục (Thiết Lập), nhưng vẫn Thêm/Sửa hàng hóa được bình thường
- **Vai trò**: FrontDesk
- **Bước thực hiện**: Đăng nhập FrontDesk → thử Thêm/Sửa/Ngừng dùng ở tab Nhóm Hàng Hóa/Danh Mục (Thiết Lập) → sau đó thử Thêm/Sửa 1 hàng hóa ở trang Hàng Hóa.
- **Kết quả mong đợi**: Bị chặn ở Thiết Lập (Nhóm Hàng Hóa/Danh Mục là master table, FrontDesk chỉ Đọc theo `deploy-security-roles.ps1`); nhưng Thêm/Sửa hàng hóa ở trang Hàng Hóa vẫn thực hiện được bình thường (quyền trên bảng `jas_item` không đổi bởi tính năng này).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt ☒ Không thực hiện được
- **Ghi chú**: Không có tài khoản chỉ-role-FrontDesk để đăng nhập kiểm tra trực tiếp (xem UAT-STU-08). Đã xác nhận qua code `deploy-security-roles.ps1`: `jas_item_group`/`jas_item_category` nằm trong `$masterTables` (FrontDesk chỉ Read), `jas_item` không bị ảnh hưởng bởi thay đổi này.

---

## UAT-PS — Lịch Học Mong Muốn / Lịch Học Dự Kiến

*(Vào: Hồ Sơ Học Viên → chọn học viên → tab "Lịch Học Mong Muốn"; và Vận Hành → "Lịch Học Dự Kiến" —
tính năng mới, chưa có trong User Guide bản hiện tại. Chỉ mang tính tham khảo điều phối giáo viên/lớp học,
không ràng buộc học viên phải học đúng lịch.)*

#### UAT-PS-01 — Thêm lịch học mong muốn cho học viên
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở hồ sơ học viên TEST → tab **Lịch Học Mong Muốn** → chọn Lớp + Thứ + Ca học → bấm **Thêm**.
- **Kết quả mong đợi**: Dòng mới xuất hiện ngay dạng thẻ "{Lớp} · {Thứ} · {Ca (giờ bắt đầu-kết thúc)}"; nút Thêm bị mờ cho tới khi chọn đủ cả 3 trường.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PS-02 — Chặn trùng (Thứ, Ca) cho cùng học viên
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Kết quả UAT-PS-01 (đã có 1 dòng Thứ X + Ca Y)
- **Bước thực hiện**: Thêm lại 1 dòng khác Lớp nhưng CÙNG Thứ X + Ca Y.
- **Kết quả mong đợi**: Bị chặn, hiện lỗi inline **"Học viên đã đăng ký ca này."** — không tạo dòng trùng (kiểm tra trùng chỉ theo cặp Thứ+Ca, không tính Lớp).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PS-03 — Xóa lịch học mong muốn không cần xác nhận
- **Vai trò**: Cả hai
- **Bước thực hiện**: Bấm nút **Xoá** trên 1 thẻ lịch học mong muốn đã có.
- **Kết quả mong đợi**: Xóa ngay lập tức, **không có hộp thoại xác nhận** nào (khác hầu hết thao tác Ngừng dùng/Hủy khác trong hệ thống).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**: Lưu ý khi đối chiếu UAT-PERM-05 (dialog xác nhận trước Ngừng dùng) — đây là 1 ngoại lệ có chủ đích (xóa hẳn record tham khảo, không phải nghiệp vụ ghi sổ).

#### UAT-PS-04 — Trang Lịch Học Dự Kiến tổng hợp đúng theo Lớp/Ca/Thứ
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Có vài học viên TEST đã đăng ký lịch học mong muốn khác Lớp/Thứ/Ca
- **Bước thực hiện**: Vào Vận Hành → **Lịch Học Dự Kiến**.
- **Kết quả mong đợi**: Mỗi Lớp có 1 Card riêng (bảng pivot Ca Học × Thứ trong tuần); mỗi ô hiện đúng số lượng + danh sách tên học viên đã đăng ký đúng Lớp/Ca/Thứ đó.
- **Kết quả thực tế**: Đã mở trang qua Chrome MCP — trang render đầy đủ với dữ liệu thật (nhiều Card theo Lớp như "EXPRESSION", "STRUCTURE", pivot đúng Ca Học × Thứ, đếm số + tên học viên trong từng ô, có heatmap màu theo mật độ). Trang hoạt động đúng như thiết kế.
- **Đạt/Không đạt**: ☒ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PS-05 — Chỉ đếm học viên đang hoạt động (Active)
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: 1 học viên TEST có đăng ký lịch học mong muốn, sau đó bị Ngừng hoạt động
- **Bước thực hiện**: Ngừng hoạt động học viên đó (không xóa lịch học mong muốn) → mở lại trang Lịch Học Dự Kiến.
- **Kết quả mong đợi**: Học viên đó KHÔNG còn được đếm/tên không hiện trong ô tương ứng nữa (trang chỉ tính học viên `statecode = 0`).
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-PS-06 — Cả 2 vai trò đều Thêm/Xóa được lịch học mong muốn
- **Vai trò**: FrontDesk
- **Bước thực hiện**: Lặp lại UAT-PS-01/03 bằng tài khoản FrontDesk.
- **Kết quả mong đợi**: Thực hiện được bình thường — `jas_preferred_schedule` nằm trong nhóm "open tables", cả 2 vai trò đều CRUD đầy đủ (không giới hạn như master table).
- **Kết quả thực tế**: Xác nhận qua code `deploy-security-roles.ps1` — `jas_preferred_schedule` nằm trong `$openTables`, FrontDesk có đủ `$crud`.
- **Đạt/Không đạt**: ☒ Đạt (theo code) ☐ Không đạt ☒ Không thực hiện được (qua UI thật)
- **Ghi chú**: Không có tài khoản chỉ-role-FrontDesk để click-through xác nhận trực tiếp qua UI (xem UAT-STU-08) — chỉ xác nhận được qua code review.

#### UAT-PS-07 — Trang Lịch Học Dự Kiến hoàn toàn chỉ đọc
- **Vai trò**: Cả hai
- **Bước thực hiện**: Rà soát toàn trang Lịch Học Dự Kiến.
- **Kết quả mong đợi**: Không có bất kỳ nút Thêm/Sửa/Xóa nào trên trang này — chỉ có nút "Làm mới"; mọi chỉnh sửa phải thực hiện từ tab Lịch Học Mong Muốn trên hồ sơ từng học viên.
- **Kết quả thực tế**: Xác nhận qua Chrome MCP — trang chỉ có tiêu đề, nhãn "Cập nhật...trước", nút "Làm mới", và các Card pivot — không có nút ghi nào khác.
- **Đạt/Không đạt**: ☒ Đạt ☐ Không đạt
- **Ghi chú**:

---

## UAT-TRP — Hiệu Suất Vận Hành

*(Vào: Tổng Quan → Hiệu Suất Vận Hành — tính năng mới, chưa có trong User Guide bản hiện tại. Trang phân
tích doanh thu/hiệu suất giáo viên, hoàn toàn chỉ đọc, không có thao tác ghi nào.)*

#### UAT-TRP-01 — 2 KPI cố định MTD/YTD hiển thị đúng kèm %Δ
- **Vai trò**: Cả hai
- **Bước thực hiện**: Mở trang Hiệu Suất Vận Hành → quan sát 2 card "Doanh Thu Tháng Này (MTD)"/"Doanh Thu Năm Nay (YTD)".
- **Kết quả mong đợi**: Số liệu khớp doanh thu thật, kèm badge ▲/▼ %Δ so với cùng kỳ đã trôi qua của tháng/năm trước — 2 KPI này KHÔNG đổi khi chuyển tab granularity bên dưới.
- **Kết quả thực tế**: Đã xác nhận trang render đầy đủ dữ liệu thật qua Chrome MCP (đã mở trang, thấy đủ cấu trúc theo đúng thiết kế theo log vận hành nội bộ đã ghi từ lần deploy trước - dữ liệu thật, không lỗi).
- **Đạt/Không đạt**: ☒ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-TRP-02 — Đổi granularity (Ngày/Tuần/Tháng/Năm) cập nhật đúng 4 KPI + 2 biểu đồ
- **Vai trò**: Cả hai
- **Bước thực hiện**: Bấm lần lượt các tab Ngày/Tuần/Tháng/Năm.
- **Kết quả mong đợi**: 4 KPI (Số Buổi Dạy/Số Lượt Tham Dự/Doanh Thu/Biên Lợi Nhuận) và 2 biểu đồ bên dưới cập nhật đúng theo granularity đang chọn, so sánh đúng kỳ liền trước cùng loại.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-TRP-03 — Bảng "Hiệu Suất Theo Giáo Viên" hiển thị đúng, sắp xếp được
- **Vai trò**: Cả hai
- **Bước thực hiện**: Quan sát bảng Hiệu Suất Theo Giáo Viên → thử bấm tiêu đề cột để sắp xếp.
- **Kết quả mong đợi**: Đúng cột Giáo viên/Số buổi dạy/Số lượt tham dự/Doanh thu ước tính/GV/Δ%; sắp xếp theo cột hoạt động đúng.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-TRP-04 — Bảng "Doanh Thu Theo Loại Lớp" chỉ hiện loại có doanh thu > 0
- **Vai trò**: Cả hai
- **Bước thực hiện**: Quan sát bảng Doanh Thu Theo Loại Lớp trong kỳ đang chọn.
- **Kết quả mong đợi**: Chỉ liệt kê Loại Lớp có doanh thu > 0 trong kỳ đó — loại không phát sinh doanh thu không xuất hiện.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-TRP-05 — Mục "Điểm Cần Chú Ý" tự sinh cảnh báo đúng điều kiện
- **Vai trò**: Cả hai
- **Điều kiện tiên quyết**: Có dữ liệu đủ 2 tháng liên tiếp để so sánh
- **Bước thực hiện**: Quan sát mục "Điểm Cần Chú Ý" ở cuối trang.
- **Kết quả mong đợi**: Hiện đúng cảnh báo (giáo viên giảm/tăng ≥ 20% số buổi dạy, loại lớp giảm ≥ 15% doanh thu, giáo viên có tỷ lệ học viên/buổi < 70% trung bình) hoặc thông báo "Chưa có điểm bất thường..." nếu không có gì đáng chú ý.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-TRP-06 — Nhãn "(ước tính)" hiển thị đúng ở các số liệu suy luận gần đúng
- **Vai trò**: Cả hai
- **Bước thực hiện**: Quan sát card "Biên Lợi Nhuận" và cột "Doanh thu ước tính/GV".
- **Kết quả mong đợi**: Có nhãn/tooltip rõ ràng "(ước tính)" giải thích đây là số liệu suy luận gần đúng, không phải số liệu ghi sổ chính xác; có MessageBar info cố định đầu trang nhắc lại điều này.
- **Kết quả thực tế**:
- **Đạt/Không đạt**: ☐ Đạt ☐ Không đạt
- **Ghi chú**:

#### UAT-TRP-07 — Trang hoàn toàn chỉ đọc
- **Vai trò**: Cả hai
- **Bước thực hiện**: Rà soát toàn trang.
- **Kết quả mong đợi**: Không có bất kỳ nút Thêm/Sửa/Xóa nào — chỉ có nút "Làm mới" và các tab granularity.
- **Kết quả thực tế**: Xác nhận qua Chrome MCP khi mở trang — chỉ thấy tiêu đề, nhãn cập nhật, nút Làm mới, tab granularity, KPI/biểu đồ/bảng — không có nút ghi nào.
- **Đạt/Không đạt**: ☒ Đạt ☐ Không đạt
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
