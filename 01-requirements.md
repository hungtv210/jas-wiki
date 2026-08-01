# Yêu Cầu Nghiệp Vụ (Requirements)

← [Về trang chủ](README.md)

## 1. Bối cảnh

JoiArt Studio là trung tâm dạy vẽ/nghệ thuật cần một hệ thống quản lý:
- Học viên và các gói học đã mua (theo số buổi, không theo lịch cố định).
- Điểm danh từng buổi học, tự động trừ số buổi còn lại.
- Bán khóa học và họa cụ (văn phòng phẩm/vật liệu vẽ) trong cùng một đơn hàng.
- Nhập hàng họa cụ, theo dõi tồn kho và giá vốn.
- Công nợ học viên (đã mua nhưng chưa thanh toán hết).
- Đội ngũ giáo viên (toàn thời gian/bán thời gian) phụ trách và trợ giảng từng buổi học.
- Báo cáo doanh thu, cảnh báo vận hành (sắp hết buổi, công nợ).
- Lương giáo viên (bảng lương theo kỳ, gồm lương cứng/theo buổi/thưởng/khấu trừ) và dòng tiền mặt tổng hợp của trung tâm (thu từ học viên, chi lương, chi mua hàng).
- Sửa sai cho các chứng từ ghi sổ nhầm (hủy 1 buổi điểm danh sai, đảo ngược đơn bán/phiếu nhập đã khóa sổ) mà không phá vỡ nguyên tắc chứng từ đã ghi sổ là bất biến.

## 2. Phạm vi hệ thống

### 2.1. Trong phạm vi
- Quản lý học viên (thông tin liên hệ, công nợ).
- Quản lý danh mục: Loại lớp học, Gói học (giá + số buổi + thời hạn), Ca học, Họa cụ, Giáo viên.
- Bán hàng thống nhất: 1 đơn có thể vừa bán khóa học vừa bán/cấp miễn phí họa cụ.
- Mua hàng (nhập họa cụ từ nhà cung cấp).
- Điểm danh: ghi nhận buổi học đã diễn ra, trừ buổi theo gói đã mua.
- Buổi học thử: điểm danh nhưng không trừ buổi (dùng gói học thử cấu hình riêng).
- Học nợ buổi học (tùy chọn bật/tắt): cho phép điểm danh dù đã hết buổi, số buổi còn lại có thể âm.
- Thanh toán công nợ (toàn phần hoặc từng phần).
- Đổi trạng thái học của một gói đã đăng ký (Đang học/Tạm ngưng/Đã hủy — "Hoàn thành" chỉ do hệ thống tự set khi hết buổi).
- Tra cứu chứng từ đã ghi sổ và sổ cái (bút toán tồn kho, giá vốn, buổi học, công nợ, lương, tiền mặt).
- Đối soát (tính lại số liệu cache từ sổ cái) — chỉ Admin.
- Báo cáo: doanh thu theo tháng, số học viên đang hoạt động, học viên sắp hết buổi, công nợ chưa thu, phân bổ theo loại lớp.
- Bảng lương giáo viên: tạo/ghi sổ bảng lương theo kỳ (lương cứng, theo buổi, thưởng, khấu trừ), tra cứu sổ nhân viên (Employee Ledger).
- Dòng tiền mặt: dashboard tổng hợp thu/chi tiền mặt của trung tâm (thu học viên, chi lương, chi mua hàng).
- Hủy 1 buổi điểm danh sai (FrontDesk hủy được trong ngày ghi sổ, Admin hủy được mọi lúc) — hoàn lại buổi vào số buổi còn lại của gói học, không xóa bản ghi điểm danh gốc.
- Đảo ngược đơn bán hàng/phiếu nhập họa cụ đã ghi sổ (chỉ Admin) — hoàn tồn kho/công nợ/ghi danh về trạng thái trước khi ghi sổ, mở khóa lại chứng từ gốc để sửa và ghi sổ lại; bản ghi Đã Ghi Sổ gốc vẫn được giữ nguyên, không xóa.

### 2.2. Ngoài phạm vi (đã chốt không làm)
- Không có lịch học cố định theo buổi/phòng (`class_session`) — học viên có thể học bất kỳ ca nào còn buổi, không ràng buộc theo thời khóa biểu cố định.
- Không có vai trò bảo mật "Giáo viên" riêng trong hệ thống (giáo viên là dữ liệu quản lý, không phải người dùng đăng nhập hệ thống).
- Không chuẩn hóa danh mục Nhà cung cấp (nhập tự do dạng văn bản trên phiếu mua hàng).
- Không hỗ trợ đảo ngược/hủy bảng lương đã ghi sổ (chỉ Đơn Bán Hàng, Phiếu Nhập Họa Cụ, và Điểm Danh có nghiệp vụ đảo ngược — xem mục 3.2–3.4).
- Không có nghiệp vụ "hủy khóa học đang học" riêng (khác với Đổi trạng thái học ở mục 2.1 — đó chỉ đổi cờ trạng thái, không hoàn buổi/tồn kho/công nợ).

## 3. Yêu cầu chức năng theo nghiệp vụ

### 3.1. Quản lý học viên
- Tạo/sửa hồ sơ học viên: họ tên, số điện thoại, email, ngày sinh, giới tính, địa chỉ, ghi chú.
- Ngừng hoạt động/kích hoạt lại học viên (không xóa cứng).
- Xem: công nợ hiện tại, tổng số buổi còn lại (tất cả gói đang hoạt động), danh sách gói đã đăng ký, sổ buổi học (lịch sử điểm danh), lịch sử mua họa cụ.
- Từ hồ sơ học viên có thể: **điểm danh** hoặc **tạo đơn bán hàng mới** cho học viên đó.

### 3.2. Điểm danh (nghiệp vụ trung tâm của hệ thống)
- Điểm danh thực hiện ngay trên hồ sơ học viên (không phải màn hình worksheet tách biệt).
- Khi điểm danh phải chọn:
  - Ngày điểm danh.
  - **Ca học** (bắt buộc).
  - **Giáo viên phụ trách** (bắt buộc).
  - **Trợ giảng** (không bắt buộc — có thể để trống nếu buổi đó không có trợ giảng; nếu chọn, không được trùng với giáo viên phụ trách).
  - Gói học sẽ trừ buổi (nếu học viên có nhiều gói đang hoạt động, phải chọn gói cụ thể; nếu chỉ có 1 gói, hệ thống tự chọn).
  - Hoặc đánh dấu **"Buổi học thử"** — dùng gói học thử đã cấu hình sẵn, ghi nhận có mặt nhưng **không trừ buổi thật**.
- Một học viên có thể điểm danh **nhiều ca trong cùng một ngày** với cùng một gói học — hệ thống chỉ chặn điểm danh trùng khi **cùng gói + cùng ngày + cùng ca**.
- Không cho điểm danh nếu gói học không ở trạng thái "Đang học" (Suspended/Cancelled/Completed).
- Mặc định không cho điểm danh nếu đã hết buổi (remaining ≤ 0), trừ khi bật cấu hình **"Cho phép học nợ"** — khi đó số buổi còn lại có thể xuống âm, gói học vẫn giữ trạng thái "Đang học" (không tự động Hoàn thành).
- Giáo viên phụ trách và trợ giảng được lưu theo từng buổi điểm danh và hiển thị lại trong sổ buổi học của học viên và trong lịch sử điểm danh — phục vụ tra cứu ai đã dạy buổi nào.
- **Hủy điểm danh** (sửa sai khi điểm danh nhầm): trên mỗi dòng "Sổ Buổi Học" chưa bị hủy, có nút **Hủy điểm danh** — hoàn 1 buổi vào số buổi còn lại của gói học, tự chuyển gói học từ Hoàn thành về lại Đang học nếu nhờ hoàn buổi mà còn buổi > 0. Bản ghi điểm danh gốc **không bị xóa**, chỉ được đánh dấu "Đã bị hủy" và có thêm 1 bút toán hoàn buổi liên kết ngược lại bản ghi gốc (phục vụ truy vết sau này). Nhân viên FrontDesk chỉ hủy được điểm danh **ghi sổ trong cùng ngày**; Admin hủy được **bất kỳ lúc nào**.

### 3.3. Bán hàng (Đơn Bán Hàng)
- Một đơn bán hàng gắn với **đúng 1 học viên**, được tạo từ hồ sơ học viên đó (không tạo đơn "vô chủ").
- Một đơn có thể có nhiều dòng, mỗi dòng là **Họa Cụ** hoặc **Gói Học**, trộn lẫn tự do trong cùng đơn.
- Dòng họa cụ có thể đánh dấu **"Cấp miễn phí"** (free issue) — vẫn trừ tồn kho nhưng không tính vào số tiền phải thu.
- Không cho ghi sổ (Post) nếu: chưa có dòng nào, có dòng gói học nhưng thiếu học viên, hoặc có dòng họa cụ vượt quá tồn kho hiện có.
- Sau khi ghi sổ: chứng từ khóa, không sửa/xóa dòng được nữa; mỗi gói học trong đơn trở thành 1 lượt đăng ký mới (còn nguyên số buổi theo gói); tồn kho họa cụ giảm tương ứng; công nợ học viên tăng theo số tiền phải thu (không tính phần cấp miễn phí); nếu đã thu tiền ngay, công nợ giảm tương ứng.
- **Đảo ngược ghi sổ** (chỉ Admin): dùng khi đơn bán bị ghi sổ nhầm. Hệ thống hoàn tồn kho họa cụ, hủy các lượt đăng ký gói học liên quan (chuyển sang Đã hủy), điều chỉnh lại công nợ học viên, rồi **mở khóa lại đúng đơn bán gốc** (không tạo đơn mới) để sửa và ghi sổ lại. Bản ghi Đã Ghi Sổ gốc vẫn được giữ lại nguyên vẹn (đánh dấu "Đã đảo ngược"), không xóa. **Chặn đảo ngược** nếu có bất kỳ lượt đăng ký nào trong đơn đã bị điểm danh ít nhất 1 buổi — phải hủy hết các điểm danh liên quan trước (xem mục 3.2).

### 3.4. Mua hàng (Phiếu Nhập Họa Cụ)
- Phiếu nhập có nhiều dòng, mỗi dòng là 1 họa cụ + số lượng + giá vốn.
- Sau khi ghi sổ: chứng từ khóa; tồn kho họa cụ tăng theo số lượng; giá vốn (last cost) của họa cụ cập nhật theo giá nhập gần nhất; ghi 1 khoản chi vào Dòng Tiền Mặt (xem mục 3.11).
- **Đảo ngược ghi sổ** (chỉ Admin): trừ lại tồn kho theo đúng số đã nhập, bù lại khoản chi tương ứng trong Dòng Tiền Mặt, rồi **mở khóa lại đúng phiếu nhập gốc** để sửa và ghi sổ lại. Bản ghi Đã Ghi Sổ gốc vẫn được giữ lại (đánh dấu "Đã đảo ngược"), không xóa. **Chặn đảo ngược** nếu tồn kho hiện tại của bất kỳ họa cụ nào trong phiếu không còn đủ để trừ lại (do hàng đã được bán bớt sang chỗ khác) — phải xử lý phần đã bán trước.

### 3.5. Quản lý công nợ / thanh toán
- Mỗi học viên có 1 số dư công nợ tổng hợp (`Công nợ`), tăng khi bán hàng ghi nợ, giảm khi thu tiền.
- Thu tiền hỗ trợ **thu từng phần** (không bắt buộc thu hết 1 lần) — có thể gọi nhiều lần cho đến khi hết nợ.
- Trạng thái thanh toán của đơn: Chưa thu / Còn nợ (thu một phần) / Đã thanh toán.

### 3.6. Quản lý đăng ký học (gói đã mua)
- Mỗi lượt đăng ký (1 dòng gói học đã bán) có trạng thái học: **Đang học**, **Tạm ngưng**, **Đã hủy**, **Hoàn thành**.
- Người dùng chỉ được chuyển thủ công sang Đang học/Tạm ngưng/Đã hủy — **Hoàn thành chỉ do hệ thống tự động set** khi hết buổi (và không bật học nợ).
- Đổi trạng thái không ảnh hưởng số buổi còn lại hay sổ cái buổi học.

### 3.7. Quản lý danh mục (Thiết lập)
- **Loại Lớp Học**: tên, độ tuổi phù hợp (Tất cả/4-6 tuổi/7-18 tuổi), mô tả.
- **Gói Học**: tên, thuộc loại lớp học nào, thời hạn (1/3/6 tháng), số buổi, giá bán.
- **Ca Học**: tên ca, giờ bắt đầu/kết thúc.
- **Giáo Viên**: tên, số điện thoại, hình thức làm việc (Toàn thời gian/Bán thời gian).
- Tất cả danh mục hỗ trợ Ngừng dùng/Kích hoạt lại (ẩn khỏi danh sách chọn nhưng không mất dữ liệu lịch sử).
- **Cấu hình chung**: bật/tắt "Cho phép học nợ", chọn gói học nào là "gói học thử" dùng cho tính năng buổi học thử.

### 3.8. Họa cụ (Vật tư/Văn phòng phẩm)
- Danh mục họa cụ: tên, danh mục (Sơn/Cọ/Giấy/Khung/Khác), đơn vị tính, giá bán lẻ.
- Giá vốn (last cost) và tồn kho là **số liệu hệ thống tự tính** từ lịch sử nhập/bán, người dùng không sửa tay.
- Từ hồ sơ họa cụ có thể tạo ngay phiếu nhập hàng cho họa cụ đó.

### 3.9. Báo cáo & Tra cứu
- **Bảng điều khiển (Dashboard)**: số lượt đăng ký đang hoạt động, doanh thu tháng này, số buổi học hôm nay, số lượt sắp hết buổi, danh sách chứng từ cần xử lý, cảnh báo sắp hết buổi.
- **Thống kê**: doanh thu theo tháng (khóa học + họa cụ, tính trực tiếp từ chứng từ đã ghi sổ — không dùng công thức xấp xỉ), phân bổ đăng ký theo loại lớp học, danh sách học viên sắp hết buổi, danh sách công nợ.
- **Chứng Từ Đã Ghi Sổ**: tra cứu chi tiết mọi đơn bán/phiếu nhập đã khóa sổ.
- **Sổ Cái**: 4 sổ cái chỉ đọc — Sổ cái họa cụ (nhập/xuất kho), bút toán giá trị (giá vốn/doanh thu), sổ buổi học, sổ công nợ học viên.
- **Lịch Sử Điểm Danh**: tra cứu ai đã điểm danh, ca nào, giáo viên/trợ giảng nào, theo ngày.

### 3.10. Quản lý lương giáo viên (Bảng Lương)
- Bảng lương gắn với **đúng 1 giáo viên**, theo kỳ lương + ngày chi cụ thể.
- Mỗi dòng bảng lương là 1 trong 4 loại khoản: **Lương cứng**, **Theo buổi**, **Thưởng**, **Khấu trừ** (khoản Khấu trừ nhập số tiền âm — đây là loại dòng duy nhất trong toàn hệ thống cho phép số tiền âm).
- Khi chọn giáo viên (hoặc đổi loại khoản), hệ thống tự gợi ý số tiền theo "Lương cứng mặc định"/"Đơn giá/buổi mặc định" đã cấu hình sẵn cho giáo viên đó (mục 3.7) — chỉ là gợi ý ban đầu, người dùng có thể sửa lại, không tính toán tự động.
- Sau khi ghi sổ: chứng từ khóa; ghi 1 bút toán vào **Sổ Nhân Viên** (Employee Ledger) cho giáo viên; ghi 1 khoản chi vào **Dòng Tiền Mặt** (mục 3.11).
- Chưa hỗ trợ đảo ngược/hủy bảng lương đã ghi sổ (xem mục 2.2).

### 3.11. Dòng tiền mặt (Cash Flow)
- Dashboard chỉ đọc, tổng hợp dòng tiền mặt thực tế của trung tâm — không phải công nợ (khác với mục 3.5).
- Hiển thị: Tổng Thu, Tổng Chi, Dòng Tiền Ròng của tháng hiện tại; biểu đồ Thu/Chi theo tháng (vài tháng gần nhất); danh sách giao dịch gần đây.
- Nguồn dữ liệu tự động: thu tiền học viên (mục 3.5), chi lương giáo viên (mục 3.10), chi mua hàng họa cụ (mục 3.4) — người dùng không nhập tay vào đây.

## 4. Quy tắc nghiệp vụ quan trọng (đã chốt, không thay đổi tùy tiện)

1. Một buổi học không bắt buộc theo lịch cố định — học viên còn buổi thì điểm danh được ở bất kỳ ca nào.
2. Một học viên có thể học nhiều ca trong cùng một ngày; chỉ chặn trùng khi cùng gói + cùng ngày + cùng ca.
3. Dòng điểm danh lỗi (gói không hoạt động/hết buổi/trùng) chỉ bị **bỏ qua dòng đó**, các dòng hợp lệ khác trong cùng lượt vẫn được ghi sổ bình thường — không hủy toàn bộ vì 1 dòng lỗi.
4. Buổi học thử ghi nhận có mặt nhưng tuyệt đối không trừ vào số buổi đã mua thật.
5. Chứng từ đã ghi sổ (Posted) là bất biến — không sửa/xóa, chỉ có thể tác động qua các nghiệp vụ điều chỉnh được thiết kế riêng (thu tiền, đổi trạng thái học, hủy điểm danh, đảo ngược ghi sổ đơn bán/phiếu nhập). Kể cả các nghiệp vụ điều chỉnh này cũng **không sửa/xóa bản ghi gốc** — chỉ tạo thêm bút toán bù trừ (hoàn buổi, điều chỉnh tồn kho, hoàn công nợ) và đánh dấu bản ghi gốc là đã được xử lý.
6. Chỉ Admin được thực hiện Đối Soát (Reconcile) — nghiệp vụ tính lại số liệu toàn hệ thống, không dành cho nhân viên thường.
7. Giáo viên phụ trách là bắt buộc trên mọi lượt điểm danh; trợ giảng luôn là tùy chọn.
8. Đảo ngược ghi sổ (đơn bán/phiếu nhập) chỉ dành cho Admin; hủy điểm danh dành cho cả 2 vai trò nhưng FrontDesk chỉ hủy được điểm danh ghi sổ **trong cùng ngày**, quá ngày đó phải nhờ Admin xử lý.

## 5. Người dùng & vai trò

| Vai trò | Ai sử dụng | Có thể làm |
|---|---|---|
| Admin | Chủ trung tâm/quản lý | Mọi nghiệp vụ + Đối Soát + Đảo ngược ghi sổ (đơn bán/phiếu nhập) + Hủy điểm danh (mọi thời điểm) |
| FrontDesk/Staff | Nhân viên lễ tân, phụ trách điểm danh | Mọi nghiệp vụ hằng ngày (học viên, điểm danh, bán/mua hàng, thu tiền, bảng lương, xem báo cáo) + Hủy điểm danh **trong ngày** — trừ Đối Soát và Đảo ngược ghi sổ |

Xem thiết kế kỹ thuật chi tiết tại [02 — Kiến Trúc & Thiết Kế](02-design.md).
Xem hướng dẫn thao tác từng bước tại [03 — Hướng Dẫn Sử Dụng](03-user-guide.md).
Xem bộ test case nghiệm thu tại [04 — Bộ Test Case UAT](04-uat-test-cases.md).
