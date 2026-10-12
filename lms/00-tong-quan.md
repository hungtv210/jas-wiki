# LMS JoiArt Studio — tổng quan (hệ thống thế hệ mới trên Azure)

> Phần này mô tả hệ thống **LMS** đang thay thế dần bản Power Platform / Dataverse mô tả ở các tài liệu `01`–`04` (thư mục gốc của repo này). Bản Dataverse vẫn được giữ làm đặc tả chức năng cho tới khi bỏ hẳn. Hiện LMS đang chạy trên môi trường thử nghiệm với dữ liệu giả lập, chưa vận hành chính thức.

## Một câu

Một hệ thống thống nhất cho **văn phòng, giáo viên và phụ huynh / học viên**: bán khóa học, điểm danh, thu tiền, quản lý họa cụ, trả lương, và để phụ huynh xem tranh, lịch học, học phí của con ngay trên điện thoại. Mọi con số luôn khớp nhau; chi phí không tăng theo số người dùng.

## Ba ứng dụng

| Ứng dụng | Dành cho | Dùng trên | Làm được gì |
|---|---|---|---|
| **Quản lý** (back-office) | Quản trị hệ thống, Quản lý lớp học | Máy tính | Học viên, bán khóa học, thu nợ, điểm danh, hủy / chuyển buổi, đảo ngược chứng từ, nhập hàng, lương, sổ cái, báo cáo, thiết lập, tài khoản đăng nhập |
| **Giáo viên** | Giáo viên | Điện thoại (cài lên màn hình chính) | Xem học viên đang trong ca của mình, chụp tranh, viết nhận xét, xem hồ sơ học viên |
| **Phụ huynh / học viên** | Phụ huynh, học viên | Điện thoại (cài lên màn hình chính) | Xem số buổi đã mua / đã học / còn lại, thư viện tranh, nhận xét, học phí, lịch đã đăng ký; gọi hoặc nhắn Zalo cho trung tâm |

## Vai trò

| Vai trò | Làm gì |
|---|---|
| **Quản trị hệ thống** | Mọi việc của Quản lý lớp học, thêm: sửa cấu hình chung (cho phép học nợ, giới hạn học thử / học nợ), tạo và khóa tài khoản Quản trị |
| **Quản lý lớp học** | Mọi việc vận hành hằng ngày: lễ tân, kế toán, điểm danh (cả học viên và giáo viên), học viên, bán khóa học, sắp xếp giáo viên, danh mục, đảo ngược chứng từ, lương |
| **Giáo viên** | Chỉ thấy học viên đã được văn phòng điểm danh vào ca của mình; chụp tranh, nhận xét. Không thấy tiền, số điện thoại học viên |
| **Phụ huynh / học viên** | Chỉ thấy dữ liệu của chính con mình |

## Những điểm khác biệt chính so với bản trước

1. **Học viên không bắt buộc học cố định.** Có thể đến bất kỳ ca nào; ca thường đến và đăng ký trước theo ngày chỉ để gợi ý, không ràng buộc. Điểm danh theo đúng bạn đến lớp.
2. **Văn phòng điểm danh, giáo viên chỉ thấy học viên trong ca.** Giáo viên không tự điểm danh; văn phòng điểm danh cho cả học viên và giáo viên.
3. **Số buổi luôn cộng lại từ sổ buổi học**, không lưu sẵn: đã mua, đã học, đã xóa, còn lại theo từng học viên, khóa, gói, lớp hay toàn trung tâm. Khóa đã hoàn thành hoặc hủy mà còn buổi vẫn được theo dõi; muốn bỏ buổi còn lại phải ghi một bút toán xóa có lý do.
4. **Học thử và học nợ không dùng khóa học giả.** Học thử không trừ buổi, không cần khóa. Học nợ (khi hết buổi) ghi nhận "chưa gán khóa" và tự trừ vào khóa học viên mua sau. Từ buổi thứ 2 có cảnh báo; có thể đặt giới hạn để chặn hẳn (mặc định không chặn).
5. **Đăng nhập bằng link / mã QR.** Đăng ký học viên tự tạo tài khoản học viên và phụ huynh; văn phòng gửi link hoặc cho quét QR là vào ngay, không email, không mã xác nhận. Tài khoản chỉ do trung tâm cấp.
6. **Chống sai sót số liệu**: không thu quá số tiền đơn; khách lẻ phải trả đủ; không điểm danh trùng một ca; không trả trùng lương một tháng; đảo ngược đơn hoàn lại tiền đã thu đúng tài khoản; mọi sửa sai có bút toán, không xóa dữ liệu.
7. **Nhận diện thương hiệu JoiArt Studio** trên cả ba ứng dụng: logo, màu navy – vàng, slogan, thông tin liên hệ.

## Kiến trúc (tóm tắt)

- Một dịch vụ web trên **Azure App Service** phục vụ cả ba ứng dụng và API.
- Dữ liệu trong **Azure SQL**; ảnh tranh trong **Azure Blob Storage** riêng tư, mở bằng liên kết có hạn ngắn.
- Phần xử lý nghiệp vụ (ghi sổ bán hàng, điểm danh, kho, lương, đối soát) chạy ở máy chủ, mỗi lần ghi sổ là một giao dịch nguyên tử và chống ghi trùng; sổ cái chỉ ghi thêm.
- Nhân viên văn phòng đăng nhập bằng email Microsoft (mã xác minh gửi về email); phụ huynh, học viên, giáo viên đăng nhập bằng link / QR do trung tâm cấp.
- Mọi dữ liệu gắn với một "trung tâm" (tenant) để sau này dùng được cho nhiều cơ sở.
- Không có chế độ offline: mất mạng thì báo lỗi và thử lại.

## Hiện trạng và việc còn lại

**Đã có:** toàn bộ chức năng trên, chạy thử trên môi trường thử nghiệm với dữ liệu giả lập, có kiểm thử tự động (API và giao diện) và bộ tài liệu demo từng vai trò.

**Chưa có:**
- Môi trường chạy chính thức (production), tên miền riêng, diễn tập sao lưu / khôi phục.
- Nhập danh sách học viên thật.
- Thông báo đẩy / email cho phụ huynh, thanh toán trực tuyến, hóa đơn điện tử.
- Quy tắc hết hạn khóa học (hiện theo dõi theo số buổi, chưa chặn theo thời hạn).

Xem tiếp: hướng dẫn từng bước có ảnh cho [văn phòng](10-quan-tri.md), [giáo viên](20-giao-vien.md), [phụ huynh / học viên](30-phu-huynh.md) và [quy tắc nghiệp vụ và an toàn](40-quy-tac-nghiep-vu.md).
