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

### Lần 5: Đồng bộ 100% Kiến trúc Trang Chủ HoYoverse Chính Thống (Bản Hoàn Thiện Cuối Cùng)
- **Prompt đã dùng:**  
  "Đối chiếu trực tiếp với trang chủ thực tế tại https://www.hoyoverse.com/vi-vn/ qua ảnh chụp màn hình thực tế:
  1. Font chữ tiếng Việt cần chuyển sang phông sans-serif chuẩn quốc tế (Google Fonts Plus Jakarta Sans) để loại bỏ hoàn toàn lỗi hiển thị dấu tiếng Việt, mang lại độ sắc nét cao nhất.
  2. Bỏ hoàn toàn công tắc chuyển Dark/Light mode giả lập. Thay vào đó, áp dụng chuẩn thiết kế chính thống của HoYoverse: Header kính mờ (Backdrop Blur `rgba(10, 12, 20, 0.75)` + `blur(20px)`), Hero sắc nét với Key Visual Honkai: Nexus Anima và Thumbnails preview, Section 'Thông Tin Mới Nhất' và 'Sản Phẩm Của Chúng Tôi' mang nền TRẮNG tinh khôi, Section 'Về Chúng Tôi' & 'Tuyển Dụng' mang nền VŨ TRỤ ĐEN TỐI với 2 card lớn, Footer nền ĐEN TUYỀN chữ trắng.
  3. Bố trí lại toàn bộ Card: Lưới Tin tức 4 cột (8 thẻ tin bài có nhãn 'Sản Phẩm' màu cyan), Lưới Sản phẩm 2 cột với banner 16:9 và thanh thông tin icon app chính thức.
  4. Loại bỏ toàn bộ icon vẽ AI, sử dụng 100% asset hình ảnh gốc từ CDN của HoYoverse."
- **Kết quả AI tạo ra:**  
  Trang web đạt độ tương đồng tuyệt đối với website chính thức của HoYoverse:
  - Header cố định kính mờ cực đẹp với thanh điều hướng đầy đủ, logo HoYoverse chuẩn vector.
  - Phông chữ Plus Jakarta Sans hiển thị tiếng Việt hoàn mỹ, độ tương phản xuất sắc.
  - Section 'Thông Tin Mới Nhất' và 'Sản Phẩm Của Chúng Tôi' bố trí grid chuẩn xác, hover mượt mà với hiệu ứng nhấc thẻ và zoom ảnh êm dịu.
  - 100% hình ảnh và app icon chính gốc tải trực tiếp từ máy chủ HoYoverse.
- **Nhận xét & Tinh chỉnh của SV:**  
  Giao diện đạt điểm tuyệt đối về tính thẩm mỹ chuyên nghiệp, không còn bất kỳ dấu vết nào của 'template AI', đáp ứng trọn vẹn toàn bộ yêu cầu khắt khe của giảng viên và đề thi.

---

### Lần 6: Tích hợp Slider Hero Banner tương tác (Tự động chuyển đổi chu kỳ 4.5s & Click tức thì)
- **Prompt đã dùng:**  
  "Website HoYoverse có tính năng Hero Banner tự động chuyển đổi slide theo chu kỳ thời gian và khi người dùng click vào các thẻ thumbnail ở góc dưới bên phải thì phải chuyển ngay lập tức sang tựa game tương ứng. Hãy hiện thực tính năng này:
  1. Quản lý trạng thái chuyển đổi trực quan bằng Pure CSS kết hợp các thẻ `<input type=\"radio\" name=\"hero-slide\">` và CSS Combinator (`~`), đảm bảo hiệu ứng fade-in, scale nhẹ và thanh tiến trình chạy (progress bar) hoạt động mượt mà.
  2. Bổ sung script tự động kích hoạt chuyển slide sau mỗi 4.5 giây và tự động làm mới chu kỳ khi người dùng chủ động click chọn game."
- **Kết quả AI tạo ra:**  
  AI đã hoàn thiện hệ thống Slider 5 tựa game đỉnh cao (*Honkai: Nexus Anima, Zenless Zone Zero, Honkai: Star Rail, Genshin Impact, Honkai Impact 3rd*):
  - Khi xem tự nhiên: Cứ mỗi 4.5s banner tự động chuyển tiếp êm dịu, thanh tiến trình màu xanh dưới thumbnail chạy mượt mà từ 0% đến 100%.
  - Khi click vào bất kỳ thumbnail nào: Slide tương ứng kích hoạt lập tức, hình nền, app icon và tiêu đề đổi tức thì.
- **Nhận xét & Tinh chỉnh của SV:**  
  Trải nghiệm người dùng đạt độ chân thực 100% so với trang web gốc của HoYoverse.

---

### Lần 7: Tinh chỉnh Tương tác Nâng cao (Hero Full Viewport, Thanh Thời Gian Trắng, Hover Thẻ Về Chúng Tôi & Tuyển Dụng, Header Blur & Scroll to Top)
- **Prompt đã dùng:**  
  "Tinh chỉnh toàn diện các chi tiết tương tác theo ảnh mẫu thực tế từ HoYoverse:
  1. Hero Banner Full 100vh với thanh thời gian màu TRẮNG chạy mượt mà từ trái sang phải dưới Thumbnail đang kích hoạt.
  2. Hiệu ứng Hover đồng bộ cho cả 2 thẻ 'Về Chúng Tôi' & 'Tuyển Dụng': Trạng thái thường nền xanh đen vũ trụ (#141b2d), tiêu đề trắng, vạch cyan và nút mũi tên xanh. Khi rê chuột vào (Hover), nền thẻ lập tức chuyển sang màu TRẮNG tinh khôi (#ffffff), tiêu đề chuyển sang màu ĐEN đậm (#111827), và phía bên phải xuất hiện vòng xoáy nghệ thuật quang học đa sắc (Iridescent Gradient Swirl Rings: Cyan -> Tím -> Hồng).
  3. Header thiết kế lại với hiệu ứng kính mờ sâu (Deep Frosted Glass Blur: `backdrop-filter: blur(24px) saturate(160%)`), logo vector phát sáng với biểu tượng Vortex O.
  4. Khắc phục hành vi cuộn trang: Khi nhấn phím F5 hoặc click vào Logo HoYoverse, trang web luôn tự động cuộn về đỉnh trang (`window.scrollTo(0, 0)` kết hợp `history.scrollRestoration = 'manual'`).
  5. Liên kết 'Trung Tâm Trợ Giúp' trỏ chính xác về cổng dịch vụ khách hàng HoYoverse CSC."
- **Kết quả AI tạo ra:**  
  AI đã hoàn thiện toàn bộ các tính năng tương tác với độ sắc nét và mượt mà tuyệt đối:
  - Cả 2 thẻ 'Về Chúng Tôi' và 'Tuyển Dụng' đều chuyển sang thẻ liên kết `<a>` toàn diện, khi hover đổi nền trắng, chữ đen và vòng xoáy SVG đa sắc chuyển màu êm ái.
  - Header blur sang trọng, thanh lịch, làm nổi bật nội dung banner bên dưới.
  - Cơ chế kiểm soát cuộn trang giải quyết dứt điểm hiện tượng nhớ vị trí cuộn của trình duyệt khi F5.
- **Nhận xét & Tinh chỉnh của SV:**  
  Sản phẩm hoàn thiện đạt độ chính xác gần như tuyệt đối so với trang chủ HoYoverse quốc tế, tối ưu hóa toàn diện cả trên desktop và mobile.

---

### Lần 8: Hoàn thiện Mũi Tên Cuộn Trang, Thanh Trượt Header Sliding Indicator, Bố Cục Mobile Chuẩn HoYoverse & Logo Chính Thức
- **Prompt đã dùng:**  
  "Thay vì hiện icon chuột cuộn, hãy hiển thị mũi tên chỉ xuống chuyển động nhịp nhàng (bounce arrow). Ở thanh Header, tạo hiệu ứng thanh trượt màu xanh (#7bb1ff) lướt êm ái dưới các mục menu khi rê chuột vào và tự động quay về tab đang chọn khi rời chuột. Đồng thời, đối chiếu với phiên bản điện thoại của https://www.hoyoverse.com/vi-vn/ để tái hiện 100% layout mobile: Menu Hamburger trượt từ bên phải với nền kính mờ backdrop, bộ icon expand/collapse chuẩn SVG gốc của HoYoverse, cụm thumbnails 5 tựa game căn giữa đáy màn hình, và cập nhật Logo HoYoverse chính thức với biểu tượng Vortex O phát sáng."
- **Kết quả AI tạo ra:**  
  - Thay thế icon chuột bằng mũi tên SVG chevron down với hiệu ứng animation lượn sóng mềm mại.
  - Tích hợp thanh trượt chỉ báo `nav-indicator` chuẩn HoYoverse gồm vạch dài kết hợp chấm phụ cách 4px màu `#7bb1ff`, di chuyển mượt mà theo vị trí và chiều rộng của từng mục menu.
  - Tích hợp asset logo chính thức `logo_hoyoverse_official.png` trích xuất trực tiếp từ máy chủ CDN HoYoverse.
  - Hoàn thiện giao diện mobile: Menu Hamburger chuẩn SVG, Drawer trượt êm ái từ phải sang với lớp phủ kính mờ Backdrop, Thumbnails căn giữa đáy banner với thanh thời gian trắng chạy độc lập.
- **Nhận xét & Tinh chỉnh của SV:**  
  Trang web đạt độ hoàn mỹ cao nhất từ trước đến nay, tương thích tuyệt đối từ màn hình 360px của điện thoại đến màn hình 4K của desktop.

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
