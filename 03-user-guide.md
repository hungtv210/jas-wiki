# Hướng Dẫn Sử Dụng (User Guide)

← [Về trang chủ](README.md)

Tài liệu này dành cho **nhân viên lễ tân / phụ trách điểm danh lớp học** và **quản lý trung tâm** JoiArt Studio. Mỗi phần là một use case thực tế, có các bước thao tác cụ thể.

## Mục lục

1. [Bắt đầu — Làm quen với hệ thống](#1-bắt-đầu--làm-quen-với-hệ-thống)
2. [Use case: Quản lý học viên](#2-use-case-quản-lý-học-viên)
3. [Use case: Điểm danh lớp học](#3-use-case-điểm-danh-lớp-học-nghiệp-vụ-quan-trọng-nhất)
4. [Use case: Bán khóa học / họa cụ](#4-use-case-bán-khóa-học--họa-cụ)
5. [Use case: Nhập hàng họa cụ](#5-use-case-nhập-hàng-họa-cụ)
6. [Use case: Quản lý giáo viên](#6-use-case-quản-lý-giáo-viên)
7. [Use case: Thu tiền công nợ](#7-use-case-thu-tiền-công-nợ)
8. [Use case: Đổi trạng thái học của một lượt đăng ký](#8-use-case-đổi-trạng-thái-học-của-một-lượt-đăng-ký)
9. [Use case: Xem báo cáo & thống kê](#9-use-case-xem-báo-cáo--thống-kê)
10. [Use case: Thiết lập danh mục (Admin)](#10-use-case-thiết-lập-danh-mục-admin)
11. [Câu hỏi thường gặp](#11-câu-hỏi-thường-gặp)

---

## 1. Bắt đầu — Làm quen với hệ thống

Sau khi đăng nhập, bạn sẽ thấy thanh điều hướng bên trái với các mục:

- **Tổng Quan** — Bảng điều khiển (KPI hôm nay) + Thống Kê (báo cáo).
- **Vận Hành** — Đơn Bán Hàng, Phiếu Nhập Họa Cụ, Lịch Sử Điểm Danh.
- **Học Viên** — Hồ Sơ Học Viên (nơi thực hiện điểm danh).
- **Họa Cụ** — Danh mục vật tư/văn phòng phẩm.
- **Chứng Từ Đã Ghi Sổ** — Tra cứu đơn/phiếu đã khóa sổ + Sổ Cái.

Ở góc dưới bên trái có nút chuyển khu vực (Area) — chuyển sang **Admin Center** để vào **Thiết Lập** (chỉ nên dùng khi cần thêm/sửa danh mục, không dùng cho công việc hằng ngày).

> **Dữ liệu danh sách được lưu tạm trong phiên làm việc**: hầu hết các trang danh sách (Thiết Lập, Họa Cụ, Hồ Sơ Học Viên, Chứng Từ Đã Ghi Sổ, Sổ Cái, Thống Kê...) chỉ tải lại dữ liệu 1 lần rồi giữ nguyên khi bạn chuyển qua lại giữa các trang trong cùng phiên đăng nhập — nếu người khác vừa thêm/sửa dữ liệu ở nơi khác, màn hình của bạn có thể chưa cập nhật ngay. Mỗi trang đều có nút **Làm mới** kèm nhãn **"Cập nhật ... trước"** (ví dụ "vừa xong", "3 phút trước") cho biết dữ liệu đang xem cũ bao lâu — bấm **Làm mới** bất cứ khi nào nghi ngờ dữ liệu chưa mới nhất.

---

## 2. Use case: Quản lý học viên

**Vào**: Học Viên → Hồ Sơ Học Viên.

### Thêm học viên mới
1. Bấm **Thêm** ở góc trên danh sách bên trái.
2. Nhập Họ và tên (bắt buộc), số điện thoại, email, ngày sinh, giới tính, địa chỉ, ghi chú.
3. Bấm **Lưu**.

### Xem hồ sơ học viên
Chọn 1 học viên trong danh sách bên trái, khung bên phải hiển thị:
- Tổng số buổi còn lại (tất cả gói đang hoạt động cộng lại), công nợ, trạng thái hoạt động.
- 2 nút thao tác nổi bật: **Điểm danh** và **Tạo đơn bán hàng**.
- 4 tab tra cứu: **Sổ Buổi Học** (mặc định, sắp xếp mới nhất trước), **Ghi Danh** (các gói đã mua), **Công Nợ**, **Lịch Sử Mua Họa Cụ**.

### Ngừng hoạt động một học viên
Bấm nút **Ngừng hoạt động** — hệ thống sẽ hỏi xác nhận trước khi thực hiện (học viên chỉ bị ẩn khỏi danh sách mặc định, có thể **Kích hoạt lại** bất kỳ lúc nào).

---

## 3. Use case: Điểm danh lớp học (nghiệp vụ quan trọng nhất)

**Vào**: Học Viên → Hồ Sơ Học Viên → chọn học viên → bấm **Điểm danh**.

### Điểm danh thông thường
1. Nếu học viên có nhiều gói đang hoạt động, chọn **Khóa đã mua** cần trừ buổi (nếu chỉ có 1 gói, hệ thống tự chọn sẵn).
2. Chọn **Ngày điểm danh** (mặc định hôm nay).
3. Chọn **Ca học** (bắt buộc).
4. Chọn **Giáo viên phụ trách** (bắt buộc — hệ thống tự chọn giáo viên đầu tiên trong danh sách, đổi lại nếu cần).
5. Chọn **Trợ giảng** nếu buổi đó có trợ giảng (không bắt buộc, để "Không có" nếu không có).
6. Bấm **Điểm danh**.
7. Hệ thống báo kết quả:
   - **"Đã điểm danh... Số buổi còn lại: X"** — thành công, đã trừ 1 buổi.
   - **"Hệ thống đã bỏ qua yêu cầu này..."** — học viên đã được điểm danh cho đúng gói này, đúng ngày, đúng ca này rồi (tránh điểm danh trùng do bấm 2 lần).

> **Lưu ý**: một học viên **có thể điểm danh nhiều ca trong cùng 1 ngày** (ví dụ sáng + chiều) với cùng 1 gói học — hệ thống chỉ chặn khi trùng cả 3 yếu tố gói + ngày + ca.

### Điểm danh buổi học thử
1. Bật công tắc **"Buổi học thử"** trong hộp thoại điểm danh.
2. Hệ thống tự dùng gói học thử đã cấu hình sẵn (xem [mục 10](#10-use-case-thiết-lập-danh-mục-admin)) — không cần chọn gói.
3. Vẫn cần chọn Ca học + Giáo viên phụ trách (+ Trợ giảng nếu có).
4. Bấm **Điểm danh** — buổi học thử được ghi nhận có mặt nhưng **không trừ vào số buổi đã mua thật** của học viên.

> Nếu công tắc "Buổi học thử" bị mờ/không bật được, nghĩa là Admin chưa cấu hình gói học thử ở Thiết Lập → Cấu Hình.

### Điểm danh khi đã hết buổi (học nợ)
- Nếu học viên đã hết buổi và tính năng **"Cho phép học nợ"** đang **tắt** (mặc định) → hệ thống báo *"Học viên không có gói học nào đang hoạt động và còn buổi"*, không cho điểm danh. Cần bán thêm gói học mới cho học viên (xem mục 4).
- Nếu Admin đã **bật** "Cho phép học nợ" ở Thiết Lập → Cấu Hình → vẫn điểm danh được, số buổi còn lại sẽ hiển thị **số âm** (ví dụ "-1 buổi") để nhắc học viên đang nợ buổi, gói học vẫn giữ trạng thái Đang học.

### Xem lại lịch sử điểm danh
- **Sổ Buổi Học** trên hồ sơ học viên: xem lịch sử điểm danh của riêng học viên đó, có cột Ca, Giáo Viên, Trợ Giảng.
- **Lịch Sử Điểm Danh** (menu Vận Hành): tra cứu theo ngày/ca cho **tất cả học viên**, dùng khi cần biết "ngày X ca Y có ai điểm danh, giáo viên nào phụ trách".

---

## 4. Use case: Bán khóa học / họa cụ

**Vào**: từ hồ sơ học viên, bấm **Tạo đơn bán hàng** (đơn luôn gắn với 1 học viên cụ thể, không tạo đơn "trống").

1. Bấm **Thêm dòng**, chọn loại dòng: **Họa Cụ** hoặc **Gói Học**.
   - Dòng Họa Cụ: chọn tên họa cụ, số lượng, đơn giá tự điền theo giá bán lẻ (có thể sửa), tick **Cấp miễn phí** nếu tặng kèm không thu tiền.
   - Dòng Gói Học: chọn Loại lớp học → Gói học cụ thể, giá/số buổi/thời hạn tự điền theo cấu hình gói.
2. Lặp lại để thêm nhiều dòng (có thể trộn Họa Cụ và Gói Học trong cùng 1 đơn).
3. Ở thanh cuối trang có 4 ô: **Tổng tiền**, **Số tiền phải thu** (không tính phần cấp miễn phí), **Số tiền đã thu**, và **Trạng thái thanh toán**.
   - Nhập **Số tiền đã thu** nếu học viên đã trả ngay — số tự động định dạng theo nghìn khi gõ (ví dụ gõ `1000000` hiện thành `1.000.000`).
   - Bấm **Nhận đủ tiền** ngay cạnh ô này để tự điền đúng số tiền phải thu (dùng khi học viên trả đủ, khỏi gõ tay).
   - Nếu số tiền đã thu khác số tiền phải thu, hệ thống hiện ngay số chênh lệch cạnh Trạng thái thanh toán (**"Thiếu X ₫"** nếu thu chưa đủ, **"Dư X ₫"** nếu thu nhiều hơn — kiểm tra lại xem có nhập nhầm không).
4. Bấm **Ghi sổ đơn hàng** — hệ thống hiện hộp thoại xác nhận, tóm tắt học viên/số dòng/tổng tiền/số tiền đã thu, kèm cảnh báo nếu có bất thường (thu thiếu, thu dư, có dòng cấp miễn phí, hoặc tổng tiền bằng 0).
5. Xác nhận **Ghi sổ** — sau bước này đơn **khóa lại, không sửa/xóa dòng được nữa**:
   - Mỗi dòng Gói Học trở thành 1 lượt đăng ký mới, đủ số buổi theo gói, sẵn sàng để điểm danh.
   - Mỗi dòng Họa Cụ trừ tồn kho tương ứng.
   - Công nợ học viên tăng theo số tiền phải thu (không tính phần cấp miễn phí).

> Không ghi sổ được nếu: đơn chưa có dòng nào, có dòng Gói Học nhưng đơn chưa xác định học viên (hiếm khi xảy ra vì đơn luôn tạo từ hồ sơ học viên), hoặc có dòng Họa Cụ vượt quá tồn kho hiện có — sửa lại số lượng hoặc nhập thêm hàng trước.

---

## 5. Use case: Nhập hàng họa cụ

**Vào**: Vận Hành → Phiếu Nhập Họa Cụ (hoặc từ hồ sơ 1 họa cụ cụ thể, bấm **Tạo phiếu mua họa cụ** để mở phiếu mới có sẵn họa cụ đó).

1. Bấm **Phiếu mới**, nhập **Nhà cung cấp** (không bắt buộc) và **Ngày nhập**.
2. Bấm **Thêm dòng**, chọn họa cụ, số lượng, giá vốn (giá nhập).
3. Lặp lại cho các họa cụ khác trong cùng phiếu.
4. Bấm **Đăng ký ghi sổ** — hộp thoại xác nhận hiện ra, cảnh báo nếu có dòng số lượng/giá vốn bằng 0 hoặc chưa nhập nhà cung cấp.
5. Xác nhận **Ghi sổ** — tồn kho các họa cụ tăng theo số lượng nhập, giá vốn (last cost) cập nhật theo giá dòng vừa nhập.

---

## 6. Use case: Quản lý giáo viên

**Vào**: Admin Center → Thiết Lập → tab **Giáo Viên**.

1. Bấm **Thêm giáo viên**.
2. Nhập Tên giáo viên (bắt buộc), Số điện thoại, chọn **Hình thức làm việc** (Toàn thời gian / Bán thời gian — bắt buộc).
3. Bấm **Lưu**.

Giáo viên sau khi thêm sẽ xuất hiện ngay trong danh sách chọn "Giáo viên phụ trách"/"Trợ giảng" khi điểm danh. Dùng nút **Ngừng dùng** nếu giáo viên nghỉ việc (ẩn khỏi danh sách chọn cho lượt điểm danh mới, không ảnh hưởng dữ liệu điểm danh cũ).

---

## 7. Use case: Thu tiền công nợ

**Vào**: Chứng Từ Đã Ghi Sổ → mở 1 đơn bán hàng đã ghi sổ và chưa thanh toán hết.

1. Bấm **Đánh dấu đã thu tiền**.
2. Nhập **Số tiền thu** (có thể thu từng phần — không bắt buộc thu hết 1 lần).
3. Bấm **Xác nhận** — công nợ học viên giảm tương ứng, trạng thái thanh toán của đơn cập nhật (Còn nợ nếu thu một phần, Đã thanh toán nếu đủ).

Có thể lặp lại thao tác này nhiều lần cho đến khi thu đủ.

---

## 8. Use case: Đổi trạng thái học của một lượt đăng ký

**Vào**: hồ sơ học viên → tab **Ghi Danh**, hoặc Chứng Từ Đã Ghi Sổ → mở đơn bán → dòng gói học.

1. Bấm **Đổi trạng thái** trên dòng gói học cần đổi.
2. Chọn trạng thái mới: **Đang học** / **Tạm ngưng** / **Đã hủy**.
3. Bấm **Xác nhận**.

> Trạng thái **Hoàn thành** không có trong danh sách chọn — hệ thống tự động chuyển sang Hoàn thành khi học viên điểm danh hết số buổi của gói (và không bật học nợ). Không thể tự đặt Hoàn thành thủ công.

---

## 9. Use case: Xem báo cáo & thống kê

- **Tổng Quan → Role Center**: xem nhanh KPI hôm nay (số đăng ký đang hoạt động, doanh thu tháng này, buổi học hôm nay, số lượt sắp hết buổi) và danh sách chứng từ cần xử lý.
- **Tổng Quan → Thống Kê**: xem doanh thu theo tháng (tách khóa học/họa cụ), phân bổ đăng ký theo loại lớp học, danh sách học viên sắp hết buổi (≤ 3 buổi), danh sách công nợ chưa thu.

---

## 10. Use case: Thiết lập danh mục (Admin)

**Vào**: chuyển Area sang **Admin Center** → Thiết Lập. Có 5 tab:

| Tab | Dùng để |
|---|---|
| Loại Lớp Học | Thêm/sửa các loại lớp (ví dụ: Foundation Studio, Advanced Studio...) |
| Gói Học | Thêm/sửa các gói học bán cho học viên (chọn thuộc loại lớp nào, số buổi, thời hạn, giá) |
| Ca Học | Thêm/sửa các ca học trong ngày (tên ca, giờ bắt đầu/kết thúc) |
| Giáo Viên | Xem [mục 6](#6-use-case-quản-lý-giáo-viên) |
| Cấu Hình | Bật/tắt "Cho phép học nợ"; chọn gói học nào dùng làm "gói học thử" |

Mỗi danh mục (trừ Cấu Hình) đều có nút **Ngừng dùng/Kích hoạt lại** — hệ thống sẽ hỏi xác nhận trước khi ngừng dùng vì sẽ ẩn khỏi danh sách chọn ở các nghiệp vụ liên quan.

---

## 11. Câu hỏi thường gặp

**Hỏi: Bấm "Điểm danh" nhưng nút bị mờ, không bấm được?**
→ Kiểm tra đã chọn đủ: Ca học và Giáo viên phụ trách (2 trường bắt buộc). Nếu học viên đang bật "Buổi học thử" mà nút vẫn mờ, kiểm tra Thiết Lập → Cấu Hình đã chọn gói học thử chưa.

**Hỏi: Điểm danh xong nhưng hệ thống báo "đã bỏ qua"?**
→ Học viên đã được điểm danh cho đúng gói + đúng ngày + đúng ca này rồi (tránh trùng do bấm nhiều lần). Nếu học viên thực sự học thêm ca khác trong ngày, hãy chọn **ca học khác** rồi điểm danh lại.

**Hỏi: Không ghi sổ được đơn bán hàng?**
→ Kiểm tra: đơn phải có ít nhất 1 dòng; nếu có dòng họa cụ, số lượng bán không được vượt tồn kho hiện có (kiểm tra lại ở trang Họa Cụ hoặc nhập thêm hàng).

**Hỏi: Tại sao danh sách chọn (giáo viên/ca học/gói học...) hiển thị đúng tên, nhưng một số màn hình cũ hơn từng hiển thị mã (ví dụ "GV-00001") thay vì tên?**
→ Đây là giới hạn của nền tảng đã được khắc phục: tên hiển thị (thân thiện) và mã (dùng nội bộ) là 2 trường khác nhau; hệ thống hiện đã hiển thị tên ở mọi nơi. Nếu vẫn thấy mã ở đâu đó, khả năng cao bản ghi đó **đã bị Ngừng dùng** (không nằm trong danh sách tên đang tải) — không phải lỗi.

**Hỏi: Ai được phép Đối Soát (Reconcile) trong Sổ Cái?**
→ Chỉ tài khoản **Admin**. Nhân viên thường (FrontDesk/Staff) thấy nút nhưng sẽ nhận thông báo không đủ quyền nếu bấm.

**Hỏi: Xóa nhầm 1 dòng trong đơn bán/phiếu nhập thì sao?**
→ Nếu đơn/phiếu **chưa ghi sổ**, có thể **Thêm dòng** lại bình thường. Nếu **đã ghi sổ**, chứng từ đã khóa và không thể thêm/sửa/xóa dòng nữa — cần liên hệ Admin để xử lý bằng nghiệp vụ điều chỉnh phù hợp (ngoài phạm vi thao tác thông thường).
