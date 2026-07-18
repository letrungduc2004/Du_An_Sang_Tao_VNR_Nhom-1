# Dự án: "Số hóa ký ức Đổi mới"

Trang web trình bày lịch sử công cuộc Đổi mới của Việt Nam, chia thành 5 chủ đề (5 file HTML), mỗi thành viên phụ trách 1 file. Tài liệu này là **ngữ cảnh chung** — dán vào đầu prompt cho AI code (Claude, ChatGPT, Copilot...) để tất cả 5 trang thống nhất về công nghệ, thiết kế và cấu trúc mô phỏng theo phong cách của dự án tham khảo [HCM202](https://hungpd0726.github.io/HCM202/).

---

## 1. Tổng quan dự án & Cảm hứng thiết kế

- **Chủ đề chung:** Quá trình Đổi mới kinh tế - xã hội Việt Nam (1975 - 2021+), chia theo 5 giai đoạn/chương.
- **Mục đích:** Thuyết trình trên lớp (phù hợp trình chiếu máy chiếu và tương tác).
- **Cảm hứng thiết kế (Từ HCM202):**
  - **Trang chủ (`index.html`):** Sử dụng sơ đồ tư duy dạng vòng tròn (Radial Mindmap) tương tác. Người dùng click vào các nút chương để zoom/xoay mượt mà và chuyển hướng.
  - **Các trang nội dung (`chude2.html` -> `chude5.html`):** Thiết kế dạng màn hình đôi (Split-screen Odyssey):
    - *Bên trái (50%):* Bản đồ tương tác (SVG/D3.js) hoặc sơ đồ động thể hiện trực quan hóa các sự kiện tương ứng với phần nội dung hiện tại.
    - *Bên phải (50%):* Panel nội dung dạng cuộn dài (Scrollytelling) có animation xuất hiện mượt mà.
  - ** Drawer/Popup thông tin:** Khi click vào nút chi tiết (ví dụ: "Xem tiểu sử/Chi tiết sự kiện"), một bảng thông tin sẽ trượt từ cạnh phải hoặc hiện đè lên với timeline dọc chi tiết.
  - **Trải nghiệm âm thanh & hạt:** Sử dụng hạt bụi bay nhẹ ở nền (Particle canvas) và âm thanh click/nhạc chuông tương tác tự tổng hợp qua Web Audio API.

---

## 2. Danh sách 5 file & Quy ước đặt tên

| STT | File | Vai trò & Chủ đề | Bố cục đề xuất |
|---|---|---|---|
| 1 | `index.html` | **Trang chủ** & Chương I: Tiền đề & Bước ngoặt (1975 - 1986) | Radial Mindmap liên kết các chương + Tích hợp nội dung Chương I |
| 2 | `chude2.html` | Chương II: Hoàn thiện thể chế & Đẩy mạnh Đổi mới (1991 - 2016) | Split-screen Odyssey (Bản đồ cải cách & Scrollytelling) |
| 3 | `chude3.html` | Chương III: Đẩy mạnh toàn diện & Động lực từ kinh tế tư nhân (2016) | Split-screen Odyssey (Sơ đồ thành phần kinh tế & Scrollytelling) |
| 4 | `chude4.html` | Chương IV: Thành tựu và kinh nghiệm sau 35 năm Đổi mới | Split-screen Odyssey (Biểu đồ tăng trưởng GDP/Xã hội & Scrollytelling) |
| 5 | `chude5.html` | Chương V: Khát vọng hùng cường & Tầm nhìn chiến lược 2045 | Split-screen Odyssey (Timeline tương lai & Scrollytelling) |

---

## 3. Yêu cầu kỹ thuật bắt buộc (áp dụng cho CẢ 5 FILE)

### 3.1. Công nghệ & Thư viện CDN
- Mỗi chủ đề là **1 file HTML duy nhất**, tự chứa toàn bộ CSS và JavaScript (inline), không tách file riêng để dễ ghép lại.
- Chỉ sử dụng các thư viện CDN tiêu chuẩn sau (không dùng framework cần build):
  - **D3.js (v7):** `https://cdnjs.cloudflare.com/ajax/libs/d3/7.8.5/d3.min.js` (dùng vẽ sơ đồ tư duy radial, bản đồ tương tác SVG hoặc biểu đồ).
  - **GSAP:** `https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js` (dùng để mượt hóa chuyển động zoom/pan của bản đồ và hiệu ứng xuất hiện của chữ).
- Code chạy được trực tiếp khi double-click mở file bằng trình duyệt (chạy offline, không cần server).

### 3.2. Âm thanh & Hiệu ứng nền
- **Web Audio API:** Sử dụng mã JavaScript tự tạo âm thanh sóng sin/chuông (Oscillator) khi hover/click chuột để tăng độ cao cấp cho tương tác (không dùng file âm thanh rời).
- **Particle Canvas:** Tích hợp hiệu ứng hạt trôi nổi tự do (canvas nhẹ nhàng phía nền) tại trang chủ và các phần chuyển giao.

### 3.3. Hệ thống thiết kế dùng chung (Design System)

**Bảng màu:**
- Màu chủ đạo: đỏ cờ `#C8102E` (tiêu đề lớn, mốc quan trọng)
- Màu phụ: vàng đất/vàng đồng `#D4A017` (nhấn mạnh số liệu, nhánh liên kết)
- Nền: be giấy cũ `#F4EDE0` hoặc trắng ngà `#FAF7F0`
- Chữ chính: xám than `#2B2B2B`
- Tạo các hoạ tiết tem phiếu cổ điển, nét đứt hoặc nét vẽ tay bằng SVG để tăng tính hoài niệm lịch sử.

**Font chữ & Bố cục:**
- Font: `"Be Vietnam Pro"`, `"Inter"`, hoặc font hệ thống `-apple-system, sans-serif`.
- Tiêu đề section ≥ 36px, nội dung ≥ 18px để dễ theo dõi khi trình chiếu.
- Tương tác camera: Khi cuộn phần nội dung bên phải, camera (hoặc viewport SVG bên trái) tự động pan/zoom mượt mà hướng tới mốc sự kiện/tọa độ tương ứng bằng GSAP.

**Hiệu ứng chuyển động (Animation):**
- Reveal text: Chữ trượt lên từ từ và mờ dần (Slide-up + Fade-in) khi cuộn đến.
- Count-up: Các chỉ số thống kê chạy số tăng dần từ 0 khi nằm trong vùng nhìn của người dùng.
- Đường vẽ động: Vẽ các đường cong liên kết (D3.js path transition) tượng trưng cho hành trình/sự kết nối lịch sử.

### 3.4. Yêu cầu nội dung & Chất lượng code
- Không tự bịa số liệu, mốc thời gian. Nếu thiếu dữ kiện, dùng placeholder rõ ràng (ví dụ: `[CẦN BỔ SUNG]`).
- Bắt buộc có:
  - Thanh cuộn tiến trình (Progress Bar) mỏng ở đỉnh trang.
  - Nút nổi "▲ Về đầu trang" xuất hiện khi cuộn xuống.
  - Nút chuyển hướng "Chương trước / Chương sau" ở góc dưới.

---

## 4. Cách ghép 5 file thành 1 website

1. Hoàn thiện file riêng theo quy ước kỹ thuật và hệ thống màu sắc.
2. Lưu tất cả 5 file cùng cấp thư mục.
3. Liên kết các chương thông qua thẻ `<a href="chudeX.html">` hoặc liên kết trực tiếp từ các nút bấm trên Radial Mindmap của `index.html`.

---

## 5. Checklist trước khi nộp (mỗi thành viên tự kiểm tra)

- [ ] File chạy được trực tiếp bằng trình duyệt (offline, không cần server).
- [ ] Đúng bảng màu (Đỏ, Vàng đồng, Be giấy) và font chữ dùng chung.
- [ ] Sử dụng D3.js/GSAP cho hoạt cảnh mượt mà hoặc bản đồ tương tác.
- [ ] Có âm thanh phản hồi nhẹ bằng Web Audio API khi click.
- [ ] Có hiệu ứng Reveal Text và hiệu ứng chạy số (Count-up) cho dữ liệu.
- [ ] Responsive tốt trên cả màn chiếu (16:9) và điện thoại thông minh.
- [ ] Không lỗi console khi kiểm tra bằng DevTools (F12).
- [ ] Tên file đúng quy ước đặt tên ở mục 2.
