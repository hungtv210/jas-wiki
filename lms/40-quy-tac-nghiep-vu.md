# LMS JoiArt Studio — quy tắc nghiệp vụ và an toàn

## 1. Số buổi học (sổ buổi học)

Sổ buổi học chỉ ghi thêm, mỗi dòng là một sự kiện:

| Bút toán | Số buổi | Khi nào |
|---|---|---|
| Mua | +n | ghi sổ đơn bán có khóa học |
| Điểm danh | −1 | mỗi lần điểm danh (đánh dấu "đã hủy" nếu bị hủy) |
| Hoàn buổi | +1 | hủy một buổi điểm danh |
| Hủy khóa | −n | đảo ngược đơn bán |
| Xóa buổi còn lại | −n | xóa có chủ đích (hết hạn, hoàn học phí) |

- **Đã mua** = Mua + Hủy khóa; **Đã học** = điểm danh chưa hủy; **Đã xóa** = Xóa buổi còn lại; **Còn lại** = tổng mọi bút toán = Đã mua − Đã học − Đã xóa.
- Các số được cộng lại mỗi lần xem, theo bộ lọc bất kỳ (học viên, khóa đã mua, gói, khóa học, lớp, toàn trung tâm, "tính đến ngày"). **Không có số lưu sẵn** nên không thể lệch.
- Khóa Hoàn thành / Tạm dừng / Đã hủy mà còn buổi vẫn được tính vào "Còn lại"; muốn bỏ phải ghi bút toán xóa.
- Khi số buổi của một khóa về 0, khóa tự chuyển "Hoàn thành"; hủy một buổi sẽ mở lại.

## 2. Điểm danh
- Văn phòng điểm danh; giáo viên không có quyền điểm danh, chỉ thấy học viên trong ca do mình dạy hoặc trợ giảng.
- Một học viên chỉ một lượt điểm danh mỗi ngày mỗi ca (kể cả khi có nhiều khóa).
- Học viên không bắt buộc học cố định: danh sách "Đã đăng ký" / "Thường đến" chỉ là gợi ý; học viên đến ca nào điểm danh ca đó.
- **Học thử:** ghi một lượt điểm danh đánh dấu học thử; không trừ buổi, không cần khóa học.
- **Học nợ** (bật "Cho phép học nợ"): khi không còn buổi, bút toán −1 được ghi **không thuộc khóa nào**; khi học viên mua khóa, các buổi nợ cũ nhất tự gắn vào khóa vừa mua.
- **Cảnh báo / giới hạn:** từ buổi học thử thứ 2 và buổi nợ thứ 2 hệ thống cảnh báo. Quản trị hệ thống có thể đặt số buổi tối đa cho mỗi loại; để trống là không giới hạn. Có số thì điểm danh bị từ chối khi vượt.
- Hủy hoặc chuyển buổi điểm danh: mọi ngày đều được, có bút toán, không xóa.

## 3. Tiền
- Ghi sổ đơn bán: tạo chứng từ đã ghi sổ, ghi sổ cái học viên (hóa đơn và thanh toán), sổ quỹ (tiền vào), kho, sổ buổi học. Chống bấm đúp.
- **Không thu quá tổng đơn.** Khách lẻ phải trả đủ (không có công nợ để thu lại).
- Thu nợ sau: không quá số còn nợ; hai lần thu cùng lúc không bao giờ cùng được nhận.
- **Đảo ngược đơn:** chỉ khi chưa điểm danh khóa trong đơn. Hoàn kho, hủy ghi danh, xóa công nợ và **ghi chi hoàn lại tiền đã thu** vào đúng tài khoản đã nhận; sổ quỹ và công nợ của đơn đó cộng lại bằng 0. Đơn gốc mở lại để sửa và ghi sổ lại.
- **Nhập hàng:** tồn kho tăng, giá vốn theo lần nhập gần nhất, một khoản chi đúng tổng phiếu vào sổ quỹ; đảo ngược bị chặn nếu hàng đã bán bớt.
- **Lương:** gợi ý lương cứng và số buổi dạy × đơn giá (một buổi dạy = một ca trong ngày, không đếm theo số học viên). Không trả trùng lương cứng / lương theo buổi cho cùng giáo viên cùng tháng; đảo ngược được (tiền hoàn vào tài khoản đã chi, bảng gốc mở lại).
- **Đối soát:** tính lại công nợ, tồn kho và trạng thái khóa đã hết buổi từ sổ cái.

## 4. Phân quyền

| | Quản trị hệ thống | Quản lý lớp học | Giáo viên | Phụ huynh / học viên |
|---|---|---|---|---|
| Cấu hình chung, tài khoản quản trị | Sửa | Chỉ xem | — | — |
| Danh mục (lớp, khóa, gói, ca, giáo viên, họa cụ, quỹ) | Sửa | Sửa | — | — |
| Học viên, bán / thu / đảo ngược, nhập hàng, lương, đối soát | Có | Có | — | — |
| Điểm danh, hủy / chuyển điểm danh | Có | Có | Không | — |
| Tiền và số điện thoại học viên | Thấy | Thấy | Không thấy | Chỉ của con mình |
| Tranh và nhận xét | Tất cả | Tất cả | Tất cả, sửa của mình | Chỉ phần được chia sẻ, chỉ của con mình |

Quyền được kiểm tra ở máy chủ (không chỉ ẩn nút) và có kiểm thử tự động, kể cả "phụ huynh A không đọc được dữ liệu của con phụ huynh B".

## 5. Đăng nhập và tài khoản
- **Tài khoản chỉ do trung tâm cấp**: tenant đăng nhập đã đóng đăng ký tự do.
- **Link / mã QR** (phụ huynh, học viên, giáo viên): bí mật dài trong đường dẫn, chỉ lưu dấu vân tay; hiệu lực 90 ngày; dùng được trên nhiều thiết bị; mỗi thiết bị nhớ đăng nhập 180 ngày và tự gia hạn khi dùng. Link bị xóa khỏi thanh địa chỉ ngay sau khi mở.
- **Tạo lại link** làm link cũ hết hiệu lực ngay; có thể đăng xuất luôn mọi thiết bị. Khóa tài khoản là mất quyền tức thì. Link không đọc lại được (không lưu bản gốc): mất thì tạo mới.
- Link giống mật khẩu: chỉ gửi đúng người. Tài khoản link chỉ xem dữ liệu của chính mình.
- **Nhân viên văn phòng** (Quản trị hệ thống, Quản lý lớp học) đăng nhập bằng email Microsoft với mã xác minh gửi về email; không dùng link.
- Trang đăng nhập có logo, màu và lời chào của JoiArt Studio.

## 6. Nhận diện thương hiệu
Logo, màu navy – vàng, tên, slogan "Brush in Hand - Universe at Heart" và thông tin liên hệ lấy từ website joiartstudio.com, dùng thống nhất ở ba ứng dụng, biểu tượng cài lên điện thoại và trang đăng nhập.
