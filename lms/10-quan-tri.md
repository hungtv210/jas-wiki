# Back-office — quản trị hệ thống và quản lý lớp học

Ứng dụng web cho **Quản trị hệ thống** (Q) và **Quản lý lớp học** (L): `…/admin/`. Quản lý lớp học làm mọi việc vận hành (lễ tân, kế toán, điểm danh, học viên, bán khóa học, sắp xếp giáo viên, danh mục, đảo ngược chứng từ); chỉ **thiết đặt hệ thống** (cấu hình chung, tài khoản quản trị) là của Quản trị hệ thống. Ảnh chụp ngày 10/10/2026 trên dữ liệu mẫu, màn 1440×900. Số buổi, ngày giờ và mã chứng từ tự sinh sẽ khác trên dữ liệu thật.

| Mã | Case | Phút | Ai |
|---|---|---|---|
| [A1](#a1--tổng-quan) | Tổng quan: học viên, doanh thu, công nợ, sắp hết buổi | 2 | Q, L |
| [A2](#a2--học-viên) | Tìm học viên, hồ sơ và 5 tab | 4 | Q, L |
| [A3](#a3--bán-khóa-học) | Bán khóa học: giảm giá → thu tiền → ghi sổ | 6 | L |
| [A4](#a4--thu-nợ) | Thu tiền còn nợ | 3 | L |
| [A5](#a5--điểm-danh-ở-văn-phòng) | Điểm danh theo ca và theo từng học viên đến lớp; đăng ký trước (tùy chọn) | 6 | L |
| [A6](#a6--hủy-hoặc-chuyển-buổi-điểm-danh) | Hủy hoặc chuyển buổi điểm danh | 3 | L, Q |
| [A7](#a7--đảo-ngược-đơn-bán) | Đảo ngược đơn đã ghi sổ (hoàn cả tiền đã thu) | 3 | L, Q |
| [A8](#a8--nhập-họa-cụ) | Nhập họa cụ: tồn kho, giá vốn, chi quỹ | 4 | L |
| [A9](#a9--bảng-lương-giáo-viên) | Bảng lương: gợi ý từ số buổi dạy, khấu trừ | 5 | L, Q |
| [A10](#a10--sổ-cái-và-đối-soát) | Sổ quỹ, sổ cái và đối soát | 3 | L, Q |
| [A11](#a11--báo-cáo-hiệu-suất-và-lịch-học) | Báo cáo hiệu suất và lịch học dự kiến | 3 | Q |
| [A12](#a12--thiết-lập-và-mã-mời) | Học phí, cấu hình, mã mời giáo viên / phụ huynh | 4 | L, Q |
| [A13](#a13--phân-quyền) | Hai vai trò khác nhau ở đâu | 3 | Q, L |
| [A14](#a14--tổng-hợp-số-buổi) | Tổng hợp số buổi theo học viên / khóa / lớp; xóa buổi còn lại | 4 | L, Q |
| [A15](#a15--tài-khoản-đăng-nhập-linkqr) | Đăng ký học viên tự tạo tài khoản; gửi link / mã QR; tạo lại khi mất | 4 | L |

Thứ tự trình bày gợi ý: A1 → A2 → A3 → A4 → A5 → A6 → A7 → A8 → A9 → A10 → A11 → A12 → A13 → A14 → A15.

---

### A1 · Tổng quan

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| Q hoặc L | Back-office | 2 phút |

**Mục tiêu:** nhìn một màn hình biết trung tâm đang thế nào hôm nay.

1. Mở `…/admin/` (mục **Tổng quan**).

![A1 · Tổng quan](img/quan-tri/a1-1-tong-quan.jpg)

**Kết quả đúng**
- [ ] Bốn ô số liệu: học viên đang học, điểm danh hôm nay, doanh thu tháng này (kèm thu/chi), công nợ phải thu.
- [ ] Hai biểu đồ 6 tháng; hai danh sách việc cần làm: học viên **sắp hết buổi** (nhắc đăng ký khóa mới) và họa cụ sắp hết.

<details>
<summary>Nếu bị hỏi</summary>

- *Số liệu lấy từ đâu?* Từ chính các sổ cái (công nợ, buổi học, kho, quỹ), không nhập tay.
- *Doanh thu tính khi nào?* Khi ghi sổ đơn bán; đơn bị đảo ngược không tính.

</details>

---

### A2 · Học viên

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| L | Back-office | 4 phút |

**Mục tiêu:** tìm nhanh một học viên và xem mọi thứ về bạn đó ở một chỗ.

1. **Học viên** → gõ vài chữ của tên (không cần dấu) vào ô tìm kiếm. Bấm dòng học viên.

![A2-1 · Tìm học viên](img/quan-tri/a2-1-tim-hoc-vien.jpg)

2. Hồ sơ mở ra với các con số **luôn được cộng lại từ sổ buổi học**, không có số lưu sẵn: **Đã mua**, **Đã học**, **Đã xóa** (chỉ hiện khi có), **Còn lại** = Đã mua − Đã học − Đã xóa, và **Công nợ**. Khóa đã hoàn thành, tạm dừng hay hủy mà còn buổi vẫn được tính; có cảnh báo vàng cho biết bao nhiêu buổi đang nằm ở các khóa đó.

![A2-2 · Hồ sơ học viên](img/quan-tri/a2-2-ho-so.jpg)

3. Lần lượt xem các tab: **Sổ buổi học** (từng buổi đã học/mua/hoàn), **Công nợ** (đơn và sổ công nợ, nút Thu tiền), **Lịch học** (ca thường đến và đăng ký trước theo ngày; không bắt buộc), **Tranh & nhận xét**.

![A2-3 · Sổ buổi học](img/quan-tri/a2-3-so-buoi-hoc.jpg)

![A2-4 · Công nợ](img/quan-tri/a2-4-cong-no.jpg)

![A2-5 · Lịch học](img/quan-tri/a2-5-lich-hoc.jpg)

![A2-6 · Tranh và nhận xét](img/quan-tri/a2-6-tranh.jpg)

**Kết quả đúng**
- [ ] Tìm "nguyen" ra cả "Nguyễn"; có tìm theo mã và số điện thoại.
- [ ] Đã mua − Đã học − Đã xóa = Còn lại, luôn luôn; tab Ghi danh cho thấy từng khóa: đã học, còn lại, trạng thái.
- [ ] Mọi lưới danh sách đều có: lọc từng cột, sắp xếp, chọn cột hiển thị, xuất CSV, phân trang, nút làm mới.

<details>
<summary>Nếu bị hỏi</summary>

- *Xóa học viên?* Không xóa, chỉ **Ngừng hoạt động** (dữ liệu cũ giữ nguyên, bạn không còn xuất hiện khi điểm danh/bán hàng).
- *Có sửa nhầm được không?* Mọi thay đổi tiền và buổi học đi qua sổ cái nên đều truy vết được; xem A6, A7.

</details>

---

### A3 · Bán khóa học

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| L | Back-office | 6 phút |

**Mục tiêu:** bán một gói học cho học viên Lý Văn Phát, có giảm giá, thu tiền và ghi sổ trong một màn hình.

1. **Đơn bán hàng** → **Tạo đơn mới**.

![A3-1 · Danh sách đơn](img/quan-tri/a3-1-danh-sach-don.jpg)

2. Gõ tên học viên vào ô **Học viên** (hoặc chọn từ gợi ý). Bấm **Khóa học**.

![A3-2 · Chọn học viên](img/quan-tri/a3-2-chon-hoc-vien.jpg)

3. Chọn gói học (nhóm theo Lớp · Khóa học, giá tự điền). Nhập **Giảm giá** 100.000 và lý do. Bấm **Lưu dòng**.

![A3-3 · Thêm khóa học](img/quan-tri/a3-3-them-khoa-hoc.jpg)

4. Bấm **Nhận đủ …** để điền số tiền đã thu, chọn tài khoản nhận tiền. Tổng tiền do hệ thống tính; **Đã đủ / Còn nợ** hiện ngay.

![A3-4 · Thanh toán](img/quan-tri/a3-4-thanh-toan.jpg)

5. Bấm **Ghi sổ**; hộp xác nhận nêu số dòng, tổng tiền, đã thu và các cảnh báo (ví dụ còn nợ sẽ vào công nợ học viên). Bấm **Ghi sổ** để xác nhận.

![A3-5 · Xác nhận ghi sổ](img/quan-tri/a3-5-xac-nhan-ghi-so.jpg)

6. Đơn bị khóa. Mở hồ sơ học viên → tab **Ghi danh** thấy khóa mới còn đủ số buổi.

![A3-6 · Đơn đã ghi sổ](img/quan-tri/a3-6-da-ghi-so.jpg)

![A3-7 · Khóa học mới trong hồ sơ](img/quan-tri/a3-7-khoa-hoc-moi.jpg)

**Kết quả đúng**
- [ ] Không thể thu **nhiều hơn** tổng đơn (nút Ghi sổ bị khóa, có thông báo đỏ); khách lẻ (không chọn học viên) phải trả đủ vì không có công nợ để ghi.
- [ ] Nếu học viên trước đó đã học khi hết buổi (học nợ, chưa gán khóa), lúc ghi sổ hệ thống **tự trừ các buổi đó vào khóa vừa mua** và báo trong thông báo; không cần gán tay.
- [ ] Hai người cùng thu tiền một đơn cùng lúc: chỉ một lần được nhận, không bao giờ thu quá số nợ.
- [ ] Thành tiền = đơn giá − giảm giá; tổng đơn bằng tổng các dòng (không bao giờ sai lệch so với đã lưu).
- [ ] Đơn có khóa học mà chưa chọn học viên thì nút **Ghi sổ** bị khóa, có dòng nhắc.
- [ ] Ghi sổ hai lần liên tiếp (bấm đúp) chỉ tạo **một** chứng từ.
- [ ] Học viên có thêm một ghi danh với số buổi đúng gói; công nợ = tổng đơn − đã thu.

<details>
<summary>Nếu bị hỏi</summary>

- *Họa cụ?* Bấm **Họa cụ** để thêm dòng; ghi sổ sẽ trừ tồn kho và không cho bán quá số tồn. Có thể đánh dấu **Tặng / miễn phí** (vẫn trừ kho, không tính tiền).
- *Khách vãng lai mua họa cụ?* Để trống học viên; vẫn ghi vào sổ quỹ khi có thu tiền.
- *Sửa đơn sau khi ghi sổ?* Không sửa trực tiếp; Quản trị đảo ngược (A7) rồi bán lại.

</details>

---

### A4 · Thu nợ

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| L | Back-office | 3 phút |

**Mục tiêu:** thu phần còn nợ của một đơn đã ghi sổ.

1. **Chứng từ đã ghi sổ** → tick **Chỉ đơn còn nợ** → bấm một dòng.

![A4-1 · Đơn còn nợ](img/quan-tri/a4-1-don-con-no.jpg)

2. Cửa sổ chi tiết đơn → **Thu tiền**.

![A4-2 · Chi tiết đơn](img/quan-tri/a4-2-chi-tiet-don.jpg)

3. Số tiền mặc định là toàn bộ phần nợ (bấm **Thu đủ** để điền lại); chọn tài khoản nhận → **Ghi nhận thu tiền**.

![A4-3 · Thu tiền](img/quan-tri/a4-3-thu-tien.jpg)

![A4-4 · Đã thu](img/quan-tri/a4-4-da-thu.jpg)

**Kết quả đúng**
- [ ] Không thu quá số còn nợ; thu một phần thì đơn chuyển sang **Thanh toán một phần**.
- [ ] Công nợ học viên giảm đúng số đã thu; sổ quỹ có thêm một khoản thu (A10).

---

### A5 · Điểm danh ở văn phòng

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| L | Back-office | 5 phút |

**Mục tiêu:** điểm danh đúng những học viên đến lớp, ca nào cũng được. **Văn phòng (Quản lý lớp học, Quản trị hệ thống) là nơi điểm danh cho cả học viên và giáo viên**: chọn giáo viên (và trợ giảng) dạy ca đó. Giáo viên chỉ thấy học viên đang trong ca của mình trên điện thoại (T2), không tự điểm danh.

**Nguyên tắc:** học viên **không bắt buộc học cố định**, có thể đến bất kỳ ca nào. Có đăng ký trước hay không đều được. Danh sách trong mỗi ca chỉ là **gợi ý** (Đã đăng ký cho đúng ngày đó / Thường đến vào thứ này); mặc định **không ai được chọn**, học viên đến thì tick đúng bạn đó.

1. **Điểm danh** → tab **Điểm danh theo ca**. Mỗi ca liệt kê các bạn **Đã đăng ký** (cho đúng ngày) và **Thường đến** (đúng thứ). Tick bạn nào đã đến; bạn chưa có tên thì gõ tên hoặc mã vào ô tìm ngay dưới ca để thêm (nhãn **Đến thêm**). Chọn giáo viên (và trợ giảng nếu có), bấm **Điểm danh N học viên**. Bạn có nhiều khóa còn buổi thì chọn khóa bị trừ ngay trong dòng.

![A5-1 · Điểm danh theo ca](img/quan-tri/a5-1-diem-danh-theo-ca.jpg)

2. Các bạn đã điểm danh hiện **Đã điểm danh** và bị trừ 1 buổi; ngay sau đó giáo viên của ca thấy các bạn này trong ứng dụng của mình.

![A5-2 · Kết quả](img/quan-tri/a5-2-ket-qua.jpg)

3. Từ hồ sơ một học viên bấm **Điểm danh**: chọn ca, giáo viên; tick **Buổi học thử** nếu là học thử (không trừ buổi); ghi chú buổi học.

![A5-3 · Điểm danh từng học viên](img/quan-tri/a5-3-diem-danh-tung-hoc-vien.jpg)

4. Tab **Lịch sử** liệt kê từng lượt theo khoảng ngày.

![A5-4 · Lịch sử điểm danh](img/quan-tri/a5-4-lich-su.jpg)

5. **Đăng ký trước (tùy chọn)**: hồ sơ học viên → tab **Lịch học** có hai phần: **Ca thường đến** (theo thứ, chỉ gợi ý) và **Đăng ký trước** (theo ngày cụ thể, kèm ghi chú). Đăng ký trước chỉ để trung tâm sắp xếp chỗ: không ràng buộc, không trừ buổi, bạn không đến cũng không sao. Phụ huynh thấy các buổi này trong ứng dụng (P1).

![A5-5 · Đăng ký trước](img/quan-tri/a5-5-dang-ky-truoc.jpg)

**Kết quả đúng**
- [ ] Điểm danh cùng học viên, cùng ca, cùng ngày lần hai bị từ chối (không trừ buổi lần nữa); khác ca trong ngày vẫn được.
- [ ] Học viên hết buổi: nếu bật **Cho phép học nợ** (A12) thì buổi đó được ghi **chưa gán khóa** (không có khóa học giả nào được tạo) và tự trừ vào khóa học khi học viên mua gói; nếu không bật thì báo hết buổi.
- [ ] **Cảnh báo, không chặn:** từ buổi học thử thứ 2 hoặc buổi nợ thứ 2, hệ thống hiện cảnh báo (nên đăng ký khóa học). Muốn chặn hẳn thì đặt giới hạn ở Thiết lập → Cấu hình (A12); để trống là không giới hạn.
- [ ] Buổi học thử không trừ buổi, không cần chọn khóa học và không cần cấu hình gói học thử.
- [ ] Học viên có nhiều khóa còn buổi: phải chọn khóa nào bị trừ.
- [ ] Học viên không có lịch cố định và chưa đăng ký vẫn điểm danh được ở bất kỳ ca nào (gõ tên vào ô tìm dưới ca).
- [ ] Không thể đăng ký trước cho ngày đã qua; không đăng ký trùng một ca.

<details>
<summary>Nếu bị hỏi</summary>

- *Danh sách ca lấy từ đâu?* Chỉ để gợi ý: lấy từ **Đăng ký trước** của ngày đó và **Ca thường đến** của thứ đó (A2 tab Lịch học). Không ràng buộc; học viên đến ca khác thì thêm bằng ô tìm bên dưới ca.
- *Khóa học hết hạn?* Hệ thống tính theo số buổi; khi dùng hết buổi khóa tự chuyển **Hoàn thành**.

</details>

---

### A6 · Hủy hoặc chuyển buổi điểm danh

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| L (trong ngày), Q (bất cứ lúc nào) | Back-office | 3 phút |

**Mục tiêu:** sửa nhầm điểm danh mà vẫn giữ nguyên lịch sử.

1. Hồ sơ học viên → tab **Sổ buổi học**. Mỗi buổi điểm danh còn sửa được có nút **Hủy** và **Chuyển khóa** (một nút duy nhất, kể cả buổi học nợ chưa có khóa).

![A6-1 · Sổ buổi học](img/quan-tri/a6-1-so-buoi-hoc.jpg)

2. **Hủy** → xác nhận.

![A6-2 · Xác nhận hủy](img/quan-tri/a6-2-xac-nhan-huy.jpg)

3. Buổi cũ được đánh dấu **đã hủy**, hệ thống thêm một bút toán hoàn 1 buổi; số buổi còn lại tăng lại.

![A6-3 · Đã hủy](img/quan-tri/a6-3-da-huy.jpg)

**Kết quả đúng**
- [ ] Quản lý lớp học và Quản trị hệ thống đều hủy/chuyển được buổi của mọi ngày (có bút toán, không xóa).
- [ ] Không hủy hai lần cùng một buổi. Khóa đã **Hoàn thành** mà được hoàn buổi thì tự trở lại **Đang học**.

---

### A7 · Đảo ngược đơn bán

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| L, Q | Back-office | 3 phút |

**Mục tiêu:** hủy một đơn đã ghi sổ nhầm, đúng cách kế toán (bút toán bù trừ, không xóa).

1. **Chứng từ đã ghi sổ** → mở đơn vừa bán ở A3 → **Đảo ngược**.

![A7-1 · Nút Đảo ngược](img/quan-tri/a7-1-dao-nguoc.jpg)

2. Đọc câu cảnh báo → **Đảo ngược**.

![A7-2 · Xác nhận](img/quan-tri/a7-2-xac-nhan.jpg)

![A7-3 · Đã đảo ngược](img/quan-tri/a7-3-da-dao-nguoc.jpg)

**Kết quả đúng**
- [ ] Chứng từ gốc được giữ nguyên, thêm các bút toán bù: hoàn tồn kho, hủy ghi danh, xóa công nợ và **hoàn lại tiền đã thu** (ghi chi từ đúng tài khoản đã nhận). Sau đảo ngược, sổ quỹ và công nợ của đơn đó cộng lại bằng 0. Đơn gốc mở lại để sửa và ghi sổ lại.
- [ ] Bị chặn nếu học viên **đã điểm danh** khóa trong đơn (hủy điểm danh trước, A6).
- [ ] Cả Quản lý lớp học và Quản trị hệ thống đều có nút này; giáo viên, phụ huynh thì không.

---

### A8 · Nhập họa cụ

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| L | Back-office | 4 phút |

**Mục tiêu:** nhập hàng từ nhà cung cấp, tồn kho và giá vốn tự cập nhật, tiền chi ra từ tài khoản.

1. **Phiếu nhập** → **Tạo phiếu nhập**. Nhập nhà cung cấp, bấm **Thêm dòng**: chọn hàng hóa, số lượng, đơn giá nhập.

![A8-1 · Dòng nhập](img/quan-tri/a8-1-dong-nhap.jpg)

2. Chọn **Tài khoản thanh toán** → **Ghi sổ**.

![A8-2 · Phiếu nhập](img/quan-tri/a8-2-phieu-nhap.jpg)

3. **Quản lý hàng hóa**: tồn kho tăng, giá vốn cập nhật theo đơn giá nhập gần nhất.

![A8-3 · Tồn kho](img/quan-tri/a8-3-ton-kho.jpg)

**Kết quả đúng**
- [ ] Tồn kho = tổng nhập − tổng bán; sổ quỹ có một khoản chi đúng tổng phiếu, ghi vào ngày nhận hàng.
- [ ] Đảo ngược phiếu nhập bị chặn nếu hàng đã bán bớt, không đủ tồn để trừ lại.

---

### A9 · Bảng lương giáo viên

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| L, Q | Back-office | 5 phút |

**Mục tiêu:** lập bảng lương một kỳ, với gợi ý tự tính từ số buổi đã dạy.

1. **Bảng lương** → **Tạo bảng lương** → chọn giáo viên và tháng. Hệ thống gợi ý: lương cứng và/hoặc **số buổi dạy × đơn giá buổi** (một buổi dạy = một ca trong ngày, không đếm theo số học viên). Bấm gợi ý để thêm.

![A9-1 · Gợi ý](img/quan-tri/a9-1-goi-y.jpg)

2. **Thêm khoản** để thêm thưởng hoặc **Khấu trừ** (nhập số dương, hệ thống tự lưu âm). Chọn tài khoản chi lương → **Ghi sổ**.

![A9-2 · Bảng lương](img/quan-tri/a9-2-bang-luong.jpg)

![A9-3 · Đã ghi sổ](img/quan-tri/a9-3-da-ghi-so.jpg)

**Kết quả đúng**
- [ ] Tổng lương = tổng các khoản (khấu trừ trừ đi). Gợi ý chỉ là gợi ý, sửa được; không tự ghi.
- [ ] Ghi sổ ghi một khoản chi vào sổ quỹ đúng ngày chi lương và hai bút toán sổ nhân viên (phải trả rồi đã trả).
- [ ] Không trả trùng: nếu giáo viên đã được trả lương cứng / lương theo buổi của tháng đó thì bảng lương hiện cảnh báo và ghi sổ bị chặn. Lập nhầm thì **Đảo ngược** bảng cũ ở Chứng từ đã ghi sổ (tiền hoàn lại tài khoản đã chi, bảng gốc mở lại để sửa).

---

### A10 · Sổ cái và đối soát

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| Q | Back-office | 3 phút |

**Mục tiêu:** cho thấy mọi con số có nguồn gốc, và có nút kiểm lại.

1. **Sổ cái & dòng tiền**: 6 sổ (Sổ quỹ, Công nợ học viên, Sổ buổi học, Sổ kho, Giá trị hàng, Sổ nhân viên). Sổ quỹ lọc theo tài khoản và khoảng ngày.

![A10-1 · Sổ quỹ](img/quan-tri/a10-1-so-quy.jpg)

2. **Đối soát**: tính lại công nợ, số buổi và tồn kho từ sổ cái.

![A10-2 · Xác nhận đối soát](img/quan-tri/a10-2-doi-soat.jpg)

![A10-3 · Kết quả](img/quan-tri/a10-3-ket-qua.jpg)

**Kết quả đúng**
- [ ] Sổ chỉ ghi thêm, không có nút sửa/xóa.
- [ ] Đối soát báo "Số liệu khớp sổ cái" khi mọi thứ bình thường; nếu có lệch (ví dụ sửa tay trong CSDL) sẽ báo đã sửa bao nhiêu.

---

### A11 · Báo cáo hiệu suất và lịch học

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| Q | Back-office | 3 phút |

1. **Báo cáo hiệu suất**: chọn khoảng ngày và nhóm theo ngày/tuần/tháng/năm — doanh thu (khóa học, họa cụ), giá vốn, lương, biên lợi nhuận ước tính, số buổi dạy từng giáo viên, doanh thu theo lớp.

![A11-1 · Báo cáo](img/quan-tri/a11-1-bao-cao.jpg)

2. **Lịch học dự kiến**: bảng tuần theo ca và thứ, tổng hợp từ lịch học đã đăng ký của từng học viên; bấm ô để xem danh sách tên.

![A11-2 · Lịch học dự kiến](img/quan-tri/a11-2-lich-hoc.jpg)

<details>
<summary>Nếu bị hỏi</summary>

- *Biên lợi nhuận chính xác không?* Là ước tính theo kỳ (doanh thu trừ giá vốn họa cụ và lương cùng kỳ), không gắn từng buổi học với từng khoản lương.
- *Buổi dạy tính thế nào?* Đếm ca (ngày + ca + giáo viên), không đếm số học viên; cột "lượt học viên" đếm riêng.

</details>

---

### A12 · Thiết lập và mã mời

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| Q | Back-office | 4 phút |

1. **Thiết lập** → **Học phí (gói học)**: Lớp → Khóa học → Gói học, giá từng gói. Các tab còn lại: Ca học, Giáo viên, Tài khoản (tiền mặt, ngân hàng), và danh mục họa cụ ở **Quản lý hàng hóa**.

![A12-1 · Học phí](img/quan-tri/a12-1-hoc-phi.jpg)

2. Tab **Cấu hình** (chỉ **Quản trị hệ thống** đổi được; Quản lý lớp học chỉ xem): **Cho phép học nợ** (điểm danh được khi đã hết buổi, ghi "chưa gán khóa"; khi học viên mua khóa mới, các buổi nợ **tự được trừ vào khóa vừa mua**), cùng hai **giới hạn tùy chọn**: số buổi học thử và số buổi học nợ tối đa mỗi học viên. Để trống = không giới hạn, chỉ cảnh báo từ buổi thứ 2; nhập số thì điểm danh bị chặn khi vượt.

![A12-2 · Cấu hình](img/quan-tri/a12-2-cau-hinh.jpg)

3. **Người dùng & mã mời** → **Tạo mã mời**: chọn vai trò (Giáo viên / Phụ huynh / Học viên / Quản lý lớp học; chỉ Quản trị hệ thống mời được thêm Quản trị hệ thống) và gắn với giáo viên hoặc học viên.

![A12-3 · Tạo mã mời](img/quan-tri/a12-3-tao-ma-moi.jpg)

4. Gửi mã 8 ký tự cho người được mời. Mã dùng một lần, hết hạn sau 14 ngày.

![A12-4 · Mã mời](img/quan-tri/a12-4-ma-moi.jpg)

**Kết quả đúng**
- [ ] Người được mời đăng ký bằng email rồi nhập mã ở lần đầu mở ứng dụng (T0, P0) là có đúng vai trò và đúng dữ liệu của mình.
- [ ] Có thể khóa/mở khóa tài khoản trong danh sách người dùng; không tự khóa chính mình; Quản lý lớp học không khóa được tài khoản Quản trị hệ thống.

---

### A13 · Phân quyền

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| L (đăng nhập bằng tài khoản Quản lý lớp học) | Back-office | 3 phút |

Hai vai trò nhân viên: **Quản lý lớp học** làm mọi việc vận hành hằng ngày và toàn quyền trên dữ liệu; **Quản trị hệ thống** có thêm quyền thiết đặt hệ thống.

1. Đăng nhập bằng tài khoản **Quản lý lớp học**: thanh bên có đủ các mục vận hành, sổ sách, Thiết lập danh mục và Người dùng.

![A13-1 · Quản lý lớp học](img/quan-tri/a13-1-quan-ly-lop.jpg)

2. Mở một đơn đã ghi sổ: có **Thu tiền** và **Đảo ngược**.

![A13-2 · Đảo ngược chứng từ](img/quan-tri/a13-2-dao-nguoc.jpg)

3. **Thiết lập → Cấu hình**: chỉ xem. Cho phép học nợ và các giới hạn học thử / học nợ là thiết đặt hệ thống, do Quản trị hệ thống đổi.

![A13-3 · Cấu hình chỉ xem](img/quan-tri/a13-3-cau-hinh-chi-xem.jpg)

**Bảng quyền**

| | Quản trị hệ thống | Quản lý lớp học | Giáo viên | Phụ huynh / học viên |
|---|---|---|---|---|
| Cấu hình chung (cho phép học nợ, giới hạn học thử / học nợ) | **Sửa** | Chỉ xem | — | — |
| Tạo tài khoản Quản trị hệ thống, khóa/mở khóa tài khoản đó | **Có** | Không | — | — |
| Danh mục (lớp, khóa học, gói học, ca, giáo viên, họa cụ, tài khoản quỹ) | Sửa | Sửa | Chỉ xem một phần | — |
| Học viên, bán khóa học, thu nợ, nhập hàng, bảng lương | Có | Có | — | — |
| Điểm danh cả học viên và giáo viên; hủy / chuyển điểm danh mọi ngày | Có | Có | Không điểm danh; chỉ thấy học viên trong ca của mình | — |
| Đảo ngược đơn bán, phiếu nhập, bảng lương; đối soát; mời giáo viên, phụ huynh | Có | Có | Không | — |
| Tiền và số điện thoại học viên | Thấy | Thấy | **Không thấy** | Chỉ của con mình |
| Tranh và nhận xét | Thấy hết | Thấy hết | Thấy hết, sửa của mình | Chỉ phần được chia sẻ, chỉ của con mình |

Quyền được kiểm tra ở máy chủ (không chỉ ẩn nút) và có kiểm thử tự động, kể cả "phụ huynh A không đọc được con của phụ huynh B".

---

### A14 · Tổng hợp số buổi

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| L, Q | Back-office | 4 phút |

**Mục tiêu:** cho thấy số buổi đã mua, đã học, đã xóa và còn lại của **bất kỳ đối tượng nào**, tính lại từ sổ buổi học ngay lúc xem; và cách xóa buổi còn lại của một khóa.

1. **Sổ sách → Tổng hợp số buổi**. Chọn **Xem theo** (học viên, khóa đã mua, gói, khóa học, lớp, hoặc tổng toàn trung tâm) và lọc thêm theo học viên, lớp, khóa học, gói, trạng thái khóa, hoặc **Tính đến ngày**. Bốn ô trên cùng là tổng của đúng bộ lọc đó.

![A14-1 · Theo học viên](img/quan-tri/a14-1-tong-hop-theo-hoc-vien.jpg)

2. Đổi **Xem theo** sang **Từng lớp**: cùng một nguồn số liệu, gộp khác đi.

![A14-2 · Theo lớp](img/quan-tri/a14-2-tong-hop-theo-lop.jpg)

3. Muốn bỏ số buổi còn lại của một khóa (hết hạn, hoàn học phí…): hồ sơ học viên → tab **Ghi danh** → **Xóa buổi còn lại** → nhập lý do. Hệ thống ghi **một bút toán xóa riêng** trong sổ buổi học (hiện ở Sổ buổi học là "Xóa buổi còn lại"), không sửa số cũ.

![A14-3 · Xóa buổi còn lại](img/quan-tri/a14-3-xoa-buoi-con-lai.jpg)

**Kết quả đúng**
- [ ] Khóa **Hoàn thành / Tạm dừng / Đã hủy** mà còn buổi vẫn có mặt trong "Còn lại" (lọc **Trạng thái khóa** để tách riêng).
- [ ] Sau khi xóa buổi còn lại: "Đã xóa" tăng, "Còn lại" về 0, Đã mua − Đã học − Đã xóa vẫn bằng Còn lại; xóa lần hai bị từ chối (không còn buổi).
- [ ] **Tính đến ngày** trong quá khứ cho ra số buổi đúng tại ngày đó.
- [ ] Hủy điểm danh hoặc đảo ngược đơn tạo bút toán riêng (Hoàn buổi, Hủy khóa) và cộng lại đúng trong mọi cách xem.

<details>
<summary>Nếu bị hỏi</summary>

- *Số "còn lại" có lưu sẵn không?* Không. Mỗi lần xem hệ thống cộng các bút toán của đối tượng được chọn (mua +, điểm danh −1, hoàn +1, hủy khóa −, xóa buổi −). Vì vậy khóa nào, học viên nào, lớp nào cũng cùng một nguồn và không thể lệch nhau.
- *Khác gì nút Đối soát?* Đối soát chỉ còn sửa số dư công nợ, tồn kho và trạng thái khóa đã hết buổi; số buổi không cần đối soát vì không lưu.

</details>

---

### A15 · Tài khoản đăng nhập (link / QR)

| Ai | Ứng dụng | Thời lượng |
|---|---|---|
| L | Back-office | 4 phút |

**Mục tiêu:** học viên và phụ huynh vào ứng dụng ngay, **không cần tự đăng ký, không email, không mã xác nhận**. Tenant đăng nhập đã đóng đăng ký tự do nên mọi tài khoản đều do trung tâm cấp.

1. **Học viên → Thêm học viên**. Ngoài thông tin học viên, form có hai ô đã tick sẵn: **Tạo tài khoản đăng nhập cho học viên** và **Tạo tài khoản cho phụ huynh** (kèm quan hệ). Bỏ tick ô nào không cần.

![A15-1 · Form đăng ký](img/quan-tri/a15-1-form-dang-ky.jpg)

2. Lưu xong hệ thống tạo các tài khoản còn thiếu và hiện **link + mã QR** của từng người. Gửi link qua Zalo, hoặc cho phụ huynh quét QR trên màn hình. Link **chỉ hiện một lần** vì hệ thống chỉ lưu dấu vân tay của nó.

*(Link và mã QR: ảnh không đăng công khai vì chứa link đăng nhập.)*

3. Sau này xem ở hồ sơ học viên → tab **Tài khoản**: ai có tài khoản, đăng nhập bằng gì, mấy thiết bị đang dùng, link còn hạn đến ngày nào. Thiếu tài khoản nào thì có nút tạo thêm.

![A15-3 · Tab Tài khoản](img/quan-tri/a15-3-tab-tai-khoan.jpg)

4. Phụ huynh mất điện thoại hoặc lộ link: **Tạo lại link / QR**, tick **đăng xuất luôn các thiết bị đang dùng**. Link cũ hết hiệu lực ngay.

![A15-4 · Tạo lại link](img/quan-tri/a15-4-tao-lai-link.jpg)

5. Giáo viên: **Người dùng & mời → Tài khoản giáo viên (link / QR)**, chọn giáo viên → link giáo viên mở thẳng app giáo viên.

**Kết quả đúng**
- [ ] Đăng ký học viên **luôn** tạo tài khoản học viên (nếu còn thiếu) và, khi tick, tài khoản phụ huynh; đăng ký lại không tạo trùng.
- [ ] Anh chị em cùng một phụ huynh: ở hồ sơ em → tab Tài khoản → **Tạo tài khoản phụ huynh** → chọn "Gắn vào tài khoản phụ huynh đã có" để một phụ huynh thấy cả hai con (không phát sinh link mới).
- [ ] Link dùng được trên nhiều thiết bị (điện thoại của ba và mẹ) cho đến khi tạo lại hoặc hết 90 ngày. Mỗi thiết bị nhớ đăng nhập 180 ngày, tự gia hạn khi dùng.
- [ ] Khóa tài khoản ở **Người dùng & mời** là mọi thiết bị mất quyền ngay.
- [ ] Phụ huynh / học viên chỉ xem dữ liệu của chính mình; không vào được màn hình văn phòng (A13).

<details>
<summary>Nếu bị hỏi</summary>

- *Có bị lộ link không?* Link hoạt động như mật khẩu: ai có link đều vào được phần của đúng người đó (xem tranh, lịch, học phí; không sửa được gì quan trọng). Vì vậy chỉ gửi đúng người; mất thì tạo lại, hệ thống ghi lại ai tạo.
- *Sao không bắt xác thực hai lớp?* Phụ huynh chỉ xem dữ liệu của con và không có thao tác nguy hiểm; ép nhập mã qua email mỗi lần là rào cản lớn nhất khiến phụ huynh bỏ ứng dụng. Nhân viên văn phòng vẫn đăng nhập bằng email Microsoft.
- *Ai tự đăng ký được không?* Không. Tenant Microsoft đã đóng đăng ký tự do; tài khoản chỉ do trung tâm cấp.

</details>

