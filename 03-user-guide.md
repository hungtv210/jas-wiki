# Hướng Dẫn Sử Dụng (User Guide)

← [Về trang chủ](README.md)

Tài liệu này dành cho **nhân viên lễ tân / phụ trách điểm danh lớp học** và **quản lý trung tâm** JoiArt Studio. Mỗi phần là một use case thực tế, có các bước thao tác cụ thể.

> Đang chuẩn bị nghiệm thu (UAT)? Xem [04 — Bộ Test Case UAT](04-uat-test-cases.md) — bộ test case bám sát các use case dưới đây, có sẵn bước thực hiện + kết quả mong đợi để tick Đạt/Không đạt.

## Mục lục

1. [Bắt đầu — Làm quen với hệ thống](#1-bắt-đầu--làm-quen-với-hệ-thống)
2. [Use case: Quản lý học viên](#2-use-case-quản-lý-học-viên)
3. [Use case: Điểm danh lớp học](#3-use-case-điểm-danh-lớp-học-nghiệp-vụ-quan-trọng-nhất)
4. [Use case: Bán khóa học / họa cụ](#4-use-case-bán-khóa-học--họa-cụ)
5. [Use case: Nhập hàng họa cụ](#5-use-case-nhập-hàng-họa-cụ)
6. [Use case: Quản lý lương giáo viên (Bảng Lương)](#6-use-case-quản-lý-lương-giáo-viên-bảng-lương)
7. [Use case: Quản lý giáo viên](#7-use-case-quản-lý-giáo-viên)
8. [Use case: Thu tiền công nợ](#8-use-case-thu-tiền-công-nợ)
9. [Use case: Đổi trạng thái học của một lượt đăng ký](#9-use-case-đổi-trạng-thái-học-của-một-lượt-đăng-ký)
10. [Use case: Xem báo cáo, thống kê & dòng tiền mặt](#10-use-case-xem-báo-cáo-thống-kê--dòng-tiền-mặt)
11. [Use case: Thiết lập danh mục (Admin)](#11-use-case-thiết-lập-danh-mục-admin)
12. [Câu hỏi thường gặp](#12-câu-hỏi-thường-gặp)

---

## 1. Bắt đầu — Làm quen với hệ thống

Sau khi đăng nhập, bạn sẽ thấy thanh điều hướng bên trái với các mục:

- **Tổng Quan** — Bảng điều khiển (KPI hôm nay) + Thống Kê (báo cáo) + Dòng Tiền Mặt.
- **Vận Hành** — Đơn Bán Hàng, Phiếu Nhập Họa Cụ, Bảng Lương, Lịch Sử Điểm Danh.
- **Học Viên** — Hồ Sơ Học Viên (nơi thực hiện điểm danh + hủy điểm danh).
- **Họa Cụ** — Danh mục vật tư/văn phòng phẩm.
- **Chứng Từ Đã Ghi Sổ** — Tra cứu đơn/phiếu đã khóa sổ + thao tác Đảo ngược ghi sổ + Sổ Cái.

Ở góc dưới bên trái có nút chuyển khu vực (Area) — chuyển sang **Admin Center** để vào **Thiết Lập** (chỉ nên dùng khi cần thêm/sửa danh mục, không dùng cho công việc hằng ngày).

> **Dữ liệu danh sách được lưu tạm trong phiên làm việc**: hầu hết các trang danh sách (Thiết Lập, Họa Cụ, Hồ Sơ Học Viên, Chứng Từ Đã Ghi Sổ, Sổ Cái, Thống Kê...) chỉ tải lại dữ liệu 1 lần rồi giữ nguyên khi bạn chuyển qua lại giữa các trang trong cùng phiên đăng nhập — nếu người khác vừa thêm/sửa dữ liệu ở nơi khác, màn hình của bạn có thể chưa cập nhật ngay. Mỗi trang đều có nút **Làm mới** kèm nhãn **"Cập nhật ... trước"** (ví dụ "vừa xong", "3 phút trước") cho biết dữ liệu đang xem cũ bao lâu — bấm **Làm mới** bất cứ khi nào nghi ngờ dữ liệu chưa mới nhất.
>
> **Danh sách dài tự tải thêm khi cuộn trang**: các danh sách nhiều dữ liệu (học viên, họa cụ, chứng từ đã ghi sổ, sổ cái, bảng lương...) chỉ hiển thị 50 dòng đầu tiên; cuộn xuống gần cuối danh sách, hệ thống tự động tải thêm 50 dòng tiếp theo (có báo "Đang tải thêm..." trong lúc chờ) — không cần bấm nút nào thêm.

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
2. Hệ thống tự dùng gói học thử đã cấu hình sẵn (xem [mục 11](#11-use-case-thiết-lập-danh-mục-admin)) — không cần chọn gói.
3. Vẫn cần chọn Ca học + Giáo viên phụ trách (+ Trợ giảng nếu có).
4. Bấm **Điểm danh** — buổi học thử được ghi nhận có mặt nhưng **không trừ vào số buổi đã mua thật** của học viên.

> Nếu công tắc "Buổi học thử" bị mờ/không bật được, nghĩa là Admin chưa cấu hình gói học thử ở Thiết Lập → Cấu Hình.

### Điểm danh khi đã hết buổi (học nợ)
- Nếu học viên đã hết buổi và tính năng **"Cho phép học nợ"** đang **tắt** (mặc định) → hệ thống báo *"Học viên không có gói học nào đang hoạt động và còn buổi"*, không cho điểm danh. Cần bán thêm gói học mới cho học viên (xem mục 4).
- Nếu Admin đã **bật** "Cho phép học nợ" ở Thiết Lập → Cấu Hình → vẫn điểm danh được, số buổi còn lại sẽ hiển thị **số âm** (ví dụ "-1 buổi") để nhắc học viên đang nợ buổi, gói học vẫn giữ trạng thái Đang học.

### Xem lại lịch sử điểm danh
- **Sổ Buổi Học** trên hồ sơ học viên: xem lịch sử điểm danh của riêng học viên đó, có cột Ca, Giáo Viên, Trợ Giảng.
- **Lịch Sử Điểm Danh** (menu Vận Hành): tra cứu theo ngày/ca cho **tất cả học viên**, dùng khi cần biết "ngày X ca Y có ai điểm danh, giáo viên nào phụ trách".

### Hủy điểm danh (điểm danh nhầm)

Dùng khi điểm danh nhầm buổi/nhầm gói/nhầm học viên và cần sửa lại.

**Vào**: hồ sơ học viên → tab **Sổ Buổi Học** (hoặc Sổ Cái → tab Session Ledger nếu muốn nhìn toàn cục nhiều học viên).

1. Tìm dòng điểm danh cần hủy (loại "Điểm danh", chưa có nhãn "Đã bị hủy").
2. Bấm nút **Hủy điểm danh** trên dòng đó.
3. Hộp thoại xác nhận hiện ra: *"Hủy buổi điểm danh [mã bút toán]? Buổi học sẽ được hoàn lại vào số buổi còn lại."* — bấm xác nhận.
4. Hệ thống hoàn lại 1 buổi vào số buổi còn lại của gói học đó (nếu gói vừa chuyển Hoàn thành do hết buổi, gói sẽ tự quay lại trạng thái Đang học vì lại có buổi). Dòng điểm danh gốc vẫn còn trong lịch sử, chỉ đổi sang trạng thái "Đã bị hủy" — không mất dữ liệu.

> **Giới hạn theo vai trò**: nhân viên **FrontDesk** chỉ hủy được điểm danh **ghi sổ trong cùng ngày hôm nay**. Muốn hủy điểm danh của ngày trước đó, cần nhờ **Admin** thực hiện.

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

### Đảo ngược ghi sổ (đơn bán ghi sổ nhầm) — chỉ Admin

**Vào**: Chứng Từ Đã Ghi Sổ → mở đơn bán hàng cần đảo ngược.

1. Bấm **Đảo ngược ghi sổ** (nút này không hiển thị nếu đơn đã bị đảo ngược trước đó — sẽ thấy nhãn "Đã đảo ngược" thay vào).
2. Hộp thoại xác nhận liệt kê rõ hậu quả: tồn kho họa cụ được hoàn lại, các lượt đăng ký gói học trong đơn bị hủy (**chỉ khi chưa điểm danh buổi nào**), công nợ học viên được điều chỉnh lại, và đơn bán gốc sẽ **mở khóa để sửa/ghi sổ lại** — đọc kỹ trước khi xác nhận.
3. Xác nhận — hệ thống thực hiện, đơn Đã Ghi Sổ gốc **vẫn được giữ lại** (đánh dấu "Đã đảo ngược", không xóa), đơn bán nháp ban đầu được mở khóa lại để sửa và ghi sổ lại từ đầu.

> **Bị chặn nếu** có lượt đăng ký trong đơn đã được điểm danh ít nhất 1 buổi — hệ thống báo lỗi nêu rõ tên các lượt đăng ký đó. Cần vào hồ sơ học viên, **Hủy điểm danh** hết các buổi liên quan (mục 3) rồi mới đảo ngược được đơn.

---

## 5. Use case: Nhập hàng họa cụ

**Vào**: Vận Hành → Phiếu Nhập Họa Cụ (hoặc từ hồ sơ 1 họa cụ cụ thể, bấm **Tạo phiếu mua họa cụ** để mở phiếu mới có sẵn họa cụ đó).

1. Bấm **Phiếu mới**, nhập **Nhà cung cấp** (không bắt buộc) và **Ngày nhập**.
2. Bấm **Thêm dòng**, chọn họa cụ, số lượng, giá vốn (giá nhập).
3. Lặp lại cho các họa cụ khác trong cùng phiếu.
4. Bấm **Đăng ký ghi sổ** — hộp thoại xác nhận hiện ra, cảnh báo nếu có dòng số lượng/giá vốn bằng 0 hoặc chưa nhập nhà cung cấp.
5. Xác nhận **Ghi sổ** — tồn kho các họa cụ tăng theo số lượng nhập, giá vốn (last cost) cập nhật theo giá dòng vừa nhập, hệ thống tự ghi 1 khoản chi vào Dòng Tiền Mặt (mục 10).

### Đảo ngược ghi sổ (phiếu nhập ghi sổ nhầm) — chỉ Admin

**Vào**: Chứng Từ Đã Ghi Sổ → mở phiếu nhập họa cụ cần đảo ngược.

1. Bấm **Đảo ngược ghi sổ** (ẩn nếu phiếu đã đảo ngược trước đó).
2. Hộp thoại xác nhận nêu rõ: tồn kho các họa cụ trong phiếu sẽ bị trừ lại đúng số đã nhập, khoản chi tương ứng trong Dòng Tiền Mặt sẽ được bù lại, và phiếu nhập gốc sẽ mở khóa để sửa/ghi sổ lại.
3. Xác nhận — phiếu Đã Ghi Sổ gốc vẫn được giữ lại (đánh dấu "Đã đảo ngược"), phiếu nhập nháp ban đầu mở khóa lại để sửa và ghi sổ lại.

> **Bị chặn nếu** tồn kho hiện tại của bất kỳ họa cụ nào trong phiếu không còn đủ để trừ lại (do đã lỡ bán bớt sang chỗ khác) — hệ thống báo rõ tên họa cụ thiếu tồn kho. Cần xử lý phần đã bán trước (ví dụ nhập bù) rồi mới đảo ngược được.

---

## 6. Use case: Quản lý lương giáo viên (Bảng Lương)

**Vào**: Vận Hành → Bảng Lương.

1. Bấm **Bảng lương mới**, chọn **Giáo viên** (bắt buộc), **Kỳ lương** và **Ngày chi** (mặc định hôm nay).
2. Bấm **Thêm dòng**, chọn **Loại khoản**:
   - **Lương cứng** hoặc **Theo buổi**: khi chọn giáo viên, hệ thống tự gợi ý số tiền theo mức lương mặc định đã cấu hình cho giáo viên đó (mục 7) — chỉ là gợi ý, có thể sửa lại.
   - **Thưởng**: nhập số tiền dương.
   - **Khấu trừ**: nhập **số tiền âm** (đây là loại dòng duy nhất trong hệ thống cho phép số âm) — dùng khi cần trừ bớt lương (ví dụ đi trễ, ứng lương kỳ trước).
3. Lặp lại để thêm nhiều dòng cho cùng 1 giáo viên (ví dụ vừa Lương cứng vừa Thưởng vừa Khấu trừ trong cùng bảng lương).
4. Tổng tiền hiển thị tự động theo tổng các dòng.
5. Bấm **Đăng ký ghi sổ** — hộp thoại xác nhận tóm tắt số dòng/tổng tiền, cảnh báo nếu có dòng số tiền bằng 0 hoặc thiếu diễn giải.
6. Xác nhận **Ghi sổ** — bảng lương khóa lại; hệ thống ghi 1 bút toán vào Sổ Nhân Viên của giáo viên đó và 1 khoản chi vào Dòng Tiền Mặt (mục 10).

> Bảng lương đã ghi sổ **chưa có nghiệp vụ đảo ngược** (khác với Đơn Bán Hàng/Phiếu Nhập Họa Cụ) — nếu ghi sổ nhầm, liên hệ Admin xử lý thủ công.

---

## 7. Use case: Quản lý giáo viên

**Vào**: Admin Center → Thiết Lập → tab **Giáo Viên**.

1. Bấm **Thêm giáo viên**.
2. Nhập Tên giáo viên (bắt buộc), Số điện thoại, chọn **Hình thức làm việc** (Toàn thời gian / Bán thời gian — bắt buộc).
3. Bấm **Lưu**.

Giáo viên sau khi thêm sẽ xuất hiện ngay trong danh sách chọn "Giáo viên phụ trách"/"Trợ giảng" khi điểm danh. Dùng nút **Ngừng dùng** nếu giáo viên nghỉ việc (ẩn khỏi danh sách chọn cho lượt điểm danh mới, không ảnh hưởng dữ liệu điểm danh cũ).

---

## 8. Use case: Thu tiền công nợ

**Vào**: Chứng Từ Đã Ghi Sổ → mở 1 đơn bán hàng đã ghi sổ và chưa thanh toán hết.

1. Bấm **Đánh dấu đã thu tiền**.
2. Nhập **Số tiền thu** (có thể thu từng phần — không bắt buộc thu hết 1 lần).
3. Bấm **Xác nhận** — công nợ học viên giảm tương ứng, trạng thái thanh toán của đơn cập nhật (Còn nợ nếu thu một phần, Đã thanh toán nếu đủ).

Có thể lặp lại thao tác này nhiều lần cho đến khi thu đủ.

---

## 9. Use case: Đổi trạng thái học của một lượt đăng ký

**Vào**: hồ sơ học viên → tab **Ghi Danh**, hoặc Chứng Từ Đã Ghi Sổ → mở đơn bán → dòng gói học.

1. Bấm **Đổi trạng thái** trên dòng gói học cần đổi.
2. Chọn trạng thái mới: **Đang học** / **Tạm ngưng** / **Đã hủy**.
3. Bấm **Xác nhận**.

> Trạng thái **Hoàn thành** không có trong danh sách chọn — hệ thống tự động chuyển sang Hoàn thành khi học viên điểm danh hết số buổi của gói (và không bật học nợ). Không thể tự đặt Hoàn thành thủ công.

---

## 10. Use case: Xem báo cáo, thống kê & dòng tiền mặt

- **Tổng Quan → Role Center**: xem nhanh KPI hôm nay (số đăng ký đang hoạt động, doanh thu tháng này, buổi học hôm nay, số lượt sắp hết buổi) và danh sách chứng từ cần xử lý.
- **Tổng Quan → Thống Kê**: xem doanh thu theo tháng (tách khóa học/họa cụ), phân bổ đăng ký theo loại lớp học, danh sách học viên sắp hết buổi (≤ 3 buổi), danh sách công nợ chưa thu.
- **Tổng Quan → Dòng Tiền Mặt**: dashboard chỉ đọc, tổng hợp dòng tiền mặt thực tế của trung tâm (khác với công nợ ở mục 8) — Tổng Thu, Tổng Chi, Dòng Tiền Ròng của tháng hiện tại; biểu đồ Thu/Chi theo vài tháng gần nhất; danh sách giao dịch gần đây. Dữ liệu tự động đổ vào từ thu tiền học viên, chi lương giáo viên (mục 6), chi mua hàng họa cụ (mục 5) — không nhập tay.

---

## 11. Use case: Thiết lập danh mục (Admin)

**Vào**: chuyển Area sang **Admin Center** → Thiết Lập. Có 5 tab:

| Tab | Dùng để |
|---|---|
| Loại Lớp Học | Thêm/sửa các loại lớp (ví dụ: Foundation Studio, Advanced Studio...) |
| Gói Học | Thêm/sửa các gói học bán cho học viên (chọn thuộc loại lớp nào, số buổi, thời hạn, giá) |
| Ca Học | Thêm/sửa các ca học trong ngày (tên ca, giờ bắt đầu/kết thúc) |
| Giáo Viên | Xem [mục 7](#7-use-case-quản-lý-giáo-viên) |
| Cấu Hình | Bật/tắt "Cho phép học nợ"; chọn gói học nào dùng làm "gói học thử" |

Mỗi danh mục (trừ Cấu Hình) đều có nút **Ngừng dùng/Kích hoạt lại** — hệ thống sẽ hỏi xác nhận trước khi ngừng dùng vì sẽ ẩn khỏi danh sách chọn ở các nghiệp vụ liên quan.

---

## 12. Câu hỏi thường gặp

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
