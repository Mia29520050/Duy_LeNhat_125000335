# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)

- **Họ và tên:** Lê Nhật Duy
- **MSSV:** 125000335
- **Tên đề tài Website:** Cổng Thông Tin Vũ Trụ Trò Chơi HoYoverse (HoYoverse Official Portal Landing Page)
- **Công cụ AI đã sử dụng:** Antigravity (Gemini 3.8 Flash)

---

## 1. Yêu cầu ban đầu (System/Initial Prompt)

> **Prompt đã dùng:**  
> "Tôi muốn xây dựng một website Landing Page chuyên nghiệp, hiện đại dựa trên trang chủ chính thức của HoYoverse (bản tiếng Việt: https://www.hoyoverse.com/vi-vn/).  
> Bắt buộc tuân thủ các quy chuẩn kỹ thuật sau:  
> 1. Chỉ sử dụng HTML5 và CSS3 thuần (không sử dụng framework CSS như Bootstrap hay Tailwind; không dùng React/Vue).  
> 2. Cấu trúc chuẩn Semantic HTML5 (tối thiểu 5 thành phần: `<header>`, `<nav>`, `<main>`, `<section>` hoặc `<article>`, `<footer>`). Hạn chế tối đa việc lạm dụng thẻ `<div>` vô nghĩa.  
> 3. Kỹ thuật CSS & CSS Variables: Khai báo hệ thống biến `:root` quản lý màu sắc, phông chữ, khoảng cách, bo góc và hiệu ứng đổ bóng nhất quán. Áp dụng CSS Flexbox và CSS Grid để bố cục đáp ứng (responsive).  
> 4. Tương tác & Thư viện: Tích hợp thư viện Animate.css cho tiêu đề/Hero CTA và thư viện AOS (Animate On Scroll) cho hiệu ứng xuất hiện cuộn trang; tự viết CSS thuần cho các hiệu ứng `:hover`, `:focus` trên button và card.  
> 5. Nội dung bao gồm: Hero Section với khẩu hiệu 'Tech Otakus Save The World', Danh sách các tựa game đình đám (Genshin Impact, Honkai: Star Rail, Zenless Zone Zero, Honkai Impact 3rd, Tears of Themis, HoYoLAB), Tin tức sự kiện mới nhất, Giới thiệu tầm nhìn công nghệ của HoYoverse và Mục tuyển dụng nhân tài."

---

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration Iterations)

### Lần 1: Dựng khung Semantic HTML & CSS Variable
- **Prompt đã dùng:**  
  "Hãy phân tích và viết mã nguồn `index.html` và `style.css` đáp ứng cấu trúc ngữ nghĩa Semantic HTML5 nghiêm ngặt. Thay vì dùng `<div>` cho tất cả khối, hãy sử dụng đúng các thẻ `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<figure>`, `<figcaption>`, `<time>`, `<aside>`, `<address>` và `<footer>`. Trong `style.css`, hãy thiết lập bảng biến `:root` hoàn chỉnh gồm bảng màu Cyberpunk/Dark Gaming của HoYoverse (`--primary-color: #00d2ff`, `--secondary-color: #7928ca`, `--bg-main: #06080f`, v.v.), typography, spacing và shadows."
- **Kết quả AI tạo ra:**  
  AI đã sinh ra cấu trúc trang đầy đủ các thẻ Semantic HTML5 và khai báo biến `:root` rất chi tiết. Tuy nhiên, ở phần danh sách game và tin tức, AI ban đầu vẫn còn lồng một số thẻ `<div class="card">` bọc ngoài không cần thiết và chưa tối ưu hóa thẻ `<figure>` cho hình ảnh banner game.
- **Nhận xét & Tinh chỉnh của SV:**  
  Tôi đã nhắc AI chuẩn hóa lại:  
  1. Chuyển toàn bộ các thẻ card trò chơi và card tin tức thành thẻ `<article class="game-card">` và `<article class="news-card">`.  
  2. Bọc hình ảnh minh họa bằng thẻ ngữ nghĩa `<figure class="card-media">` và sử dụng thẻ `<time datetime="...">` cho ngày phát hành tin tức.  
  3. Bổ sung thẻ `<aside class="hero-stats">` để chứa các số liệu thống kê người chơi nổi bật.  
  4. Đảm bảo toàn bộ menu mobile có thể hoạt động hoàn toàn bằng Pure CSS (sử dụng checkbox hack `<input type="checkbox" id="nav-toggle">` kết hợp `:checked`) mà không cần đến JavaScript điều khiển giao diện.

---

### Lần 2: Tích hợp thư viện Animate.css & AOS (Animate On Scroll)
- **Prompt đã dùng:**  
  "Tích hợp thư viện Animate.css (phiên bản 4.1.1) qua CDN để tạo hiệu ứng chuyển động mượt mà cho phần Hero Header (tiêu đề chính, huy hiệu cổng thông tin và nút CTA). Đồng thời tích hợp thư viện AOS (Animate On Scroll v2.3.4) cho toàn bộ các section bên dưới với các thuộc tính `data-aos='fade-up'`, `data-aos='zoom-in'`, `data-aos-delay` phù hợp. Viết thêm các hiệu ứng `:hover`, `:focus` tự tạo bằng CSS thuần cho nút bấm và game cards (phát sáng viền neon, nhấc card lên nhẹ nhàng, zoom ảnh thumbnail mượt mà)."
- **Thách thức gặp phải:**  
  Khi liên kết AOS qua CDN, nếu các phần tử mang thuộc tính `data-aos` được render trước khi thư viện được tải hoặc khi cuộn trang nhanh, hiệu ứng đôi lúc bị giật hoặc che khuất giao diện nếu `overflow-x: hidden` trên `body` không được xử lý đồng bộ.
- **Cách sửa prompt (Debug prompt):**  
  "Hãy cấu hình script khởi tạo `AOS.init({ once: true, duration: 800, offset: 80, easing: 'ease-out-cubic' })` đặt ngay trước thẻ đóng `</body>`. Trong `style.css`, bổ sung quy tắc chống tràn trang ngang `overflow-x: hidden` trên thẻ `html, body`, đồng thời thiết lập `backdrop-filter: blur(...)` và `will-change: transform` hợp lý để hiệu ứng cuộn trang đạt chuẩn 60 FPS, chuyển động tinh tế không gây nhức mắt."

---

### Lần 3: Tinh chỉnh Responsive, UI/UX HoYoverse & Hiệu ứng tương tác Hover/Focus
- **Prompt đã dùng:**  
  "Kiểm tra tính tương thích trên các thiết bị di động (Mobile màn hình dưới 768px và Tablet dưới 1024px). Áp dụng CSS Grid tự co giãn `repeat(auto-fit, minmax(...))` cho danh sách Games và Tin tức. Đảm bảo toàn bộ liên kết và nút bấm có trạng thái `:focus-visible` với đường viền outline rõ ràng để đạt chuẩn tiếp cận người dùng (Accessibility). Tối ưu hóa đường dẫn hình ảnh nội bộ trong thư mục `assets/images/` để trang web chạy hoàn hảo khi triển khai trên GitHub Pages."
- **Kết quả AI tạo ra:**  
  Giao diện hiển thị sắc nét trên cả điện thoại, máy tính bảng và màn hình lớn. Menu điều hướng trên điện thoại trượt mượt mà từ cạnh phải sang khi nhấn nút burger. Các hình ảnh game tải nhanh chóng từ thư mục nội bộ `assets/images/`.
- **Nhận xét & Tinh chỉnh của SV:**  
  Tôi đã tinh chỉnh thêm màu gradient trên văn bản tiêu đề (`.text-gradient`), tăng độ tương phản của chữ màu xám nhạt trên nền tối để giáo viên và người chấm có thể đọc rõ ràng nội dung, đồng thời bổ sung thông tin định danh sinh viên (Họ tên, MSSV, Tên môn học) tại phần footer để minh bạch bài làm thi giữa kỳ.

---

### Lần 4: Nâng cấp Vibe Coding chuyên sâu - Thoát khỏi giao diện mẫu AI, thêm Dark/Light Mode & Accordion Game Cards
- **Prompt đã dùng:**  
  "Giao diện hiện tại trông còn hơi rập khuôn dạng template AI, chưa toát lên thần thái gaming đẳng cấp như web thật của HoYoverse. Hãy thiết kế lại toàn diện:
  1. Thêm công tắc chuyển đổi Chế độ Sáng / Tối (Dark / Light Mode) nhưng bắt buộc chỉ dùng HTML và CSS thuần (Pure CSS checkbox trick với general sibling combinator `~`), tuyệt đối không dùng JavaScript.
  2. Tái hiện phong cách Accordion Flex Cards mở rộng khi hover đặc trưng của HoYoverse cho khu vực danh sách Game (mặc định thẻ đầu mở rộng, khi rê chuột vào thẻ nào thì thẻ đó bung rộng mượt mà với hiệu ứng shimmer tia sáng).
  3. Hoàn thiện Responsive di động với Drawer Navigation trượt mượt mà, đầy đủ các breakpoint (480px, 768px, 1024px, 1280px).
  4. Nâng tầm Typography với Google Fonts (Outfit & DM Serif Display) và viền ánh sáng tinh tế."
- **Kết quả AI tạo ra:**  
  AI đã tái cấu trúc toàn diện `index.html` và `style.css`:
  - Cơ chế Dark/Light Mode thuần CSS cực kỳ sáng tạo: đặt `<input type="checkbox" id="theme-ctl">` ngay trước `.site-wrap`, khi kích hoạt checkbox thì toàn bộ hệ thống biến `:root` được ghi đè sang bảng màu sáng dịu mắt (Light Mode).
  - Phần Featured Games được chuyển đổi thành hệ thống Accordion Flex Cards ấn tượng: thẻ game đang kích hoạt tự động giãn rộng chiếm tỷ lệ `flex: 4`, các thẻ phụ thu gọn `flex: 1`, khi hover thẻ nào thẻ đó phóng to kèm lớp phủ ánh sáng shimmer sang trọng.
  - Menu burger trên điện thoại cũng sử dụng checkbox hack thuần CSS, đóng mở êm ái mà không cần bất kỳ dòng mã JavaScript nào.
- **Nhận xét & Tinh chỉnh của SV:**  
  Trang web hoàn toàn lột xác, mang đậm phong cách HoYoverse chính thống, loại bỏ triệt để cảm giác 'AI template', đáp ứng 100% tiêu chí đề thi: vừa đẹp mắt, vừa đúng chuẩn kỹ thuật Semantic HTML5, CSS thuần, Responsive và đầy đủ hiệu ứng tương tác.

---

## 3. Đánh giá cá nhân về quá trình Vibe Coding

### AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?
- **Khởi tạo hệ thống CSS Variables và Bố cục Grid/Flexbox phức tạp:** Thay vì phải tự gõ thủ công hàng chục biến màu, media queries và các thuộc tính canh chỉnh khoảng cách, AI giúp sinh ra một hệ thống thiết kế (Design System) chuẩn chỉnh chỉ trong vài giây.
- **Xây dựng cấu trúc HTML5 ngữ nghĩa lớn:** AI giúp viết toàn bộ khung thẻ chuẩn xác, lồng ghép đầy đủ các thẻ con ngữ nghĩa (`<figure>`, `<article>`, `<time>`, `<address>`) mà không bị thiếu sót thẻ đóng hay sai sót cú pháp.
- **Viết các hiệu ứng CSS chuyển động nâng cao:** AI nhanh chóng đề xuất các công thức bezier curve, box-shadow dạng glow phát sáng neon và hiệu ứng kính mờ glassmorphism đặc trưng của thương hiệu HoYoverse.

### Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web?
1. **Prompt cần cụ thể và có ràng buộc rõ ràng (Constraints):** Nếu chỉ yêu cầu 'làm website HoYoverse', AI có thể sẽ tự ý dùng Tailwind hoặc chèn mã JavaScript tùy tiện. Khi ta quy định rõ: *'Chỉ dùng HTML/CSS thuần, cấu trúc Semantic HTML5, dùng CSS Variables, tích hợp đúng Animate.css và AOS'*, AI sẽ tuân thủ nghiêm ngặt theo đúng tiêu chí chấm điểm của đề thi.
2. **Tư duy tinh chỉnh lặp lại (Iterative Refinement) là then chốt:** Không nên kỳ vọng một prompt duy nhất giải quyết tất cả. Cách tiếp cận hiệu quả nhất là chia nhỏ từng bước: Dựng khung Semantic trước -> Xây dựng hệ thống biến & Style -> Tích hợp thư viện & Hiệu ứng chuyển động -> Kiểm tra Responsive & Sửa lỗi.
3. **Người lập trình phải là người cầm lái (Vibe Control):** Dù AI viết code rất nhanh, sinh viên vẫn phải đọc hiểu từng dòng code, kiểm tra xem AI có lạm dụng thẻ `<div>` hay không, cấu trúc có chuẩn SEO và Responsive hay không để kịp thời nhắc nhở và tinh chỉnh.
