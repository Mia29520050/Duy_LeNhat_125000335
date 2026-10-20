# Cổng Thông Tin Vũ Trụ Trò Chơi HoYoverse (HoYoverse Portal Landing Page)

> **BÀI THI GIỮA KỲ - HỌC PHẦN THIẾT KẾ WEB**  
> **Trường Đại học Lạc Hồng - Khoa Công nghệ Thông tin**  
> **Sinh viên thực hiện:** Lê Nhật Duy  
> **Mã số sinh viên:** 125000335  
> **Lớp:** Công nghệ Thông tin  

---

## 🌐 Đường Dẫn Nộp Bài (Live Preview & Mã Nguồn)

* **🔗 GitHub Pages Live Preview:** [https://mia29520050.github.io/Duy_LeNhat_125000335/](https://mia29520050.github.io/Duy_LeNhat_125000335/)
* **📂 GitHub Repository:** [https://github.com/Mia29520050/Duy_LeNhat_125000335](https://github.com/Mia29520050/Duy_LeNhat_125000335)

---

## 📋 Giới Thiệu Dự Án & Yêu Cầu Kỹ Thuật

Trang web được thiết kế lấy cảm hứng từ website chính thức của **HoYoverse** ([https://www.hoyoverse.com/vi-vn/](https://www.hoyoverse.com/vi-vn/)) mang phong cách Dark Cyberpunk Gaming, hiển thị các tựa game nổi tiếng: *Genshin Impact, Honkai: Star Rail, Zenless Zone Zero, Honkai Impact 3rd, Tears of Themis* và nền tảng cộng đồng *HoYoLAB*.

### 1. Chuẩn Semantic HTML5 (Tối thiểu 5 thành phần cốt lõi)
- `<header>`: Logo HoYoverse, thanh điều hướng, chuyển đổi ngôn ngữ, nút đăng nhập.
- `<nav>`: Thanh điều hướng cuộn trang mượt mà (Trang Chủ, Trò Chơi, Tin Tức, Về Chúng Tôi, Tuyển Dụng, HoYoLAB).
- `<main>`: Khu vực nội dung chính chứa các phân đoạn chính của website.
- `<section>` & `<article>`: 
  - Hero Section (`#home`)
  - Featured Games (`#games` với 6 `<article class="game-card">`)
  - Latest News (`#news` với 4 `<article class="news-card">`)
  - About HoYoverse (`#about`)
  - Careers & Culture (`#careers`)
- `<figure>` & `<figcaption>`: Hiển thị hình ảnh minh họa chất lượng cao có chú thích và thẻ thể loại game.
- `<time>`: Thể hiện thời gian phát hành tin tức chuẩn SEO.
- `<aside>`: Thống kê nhanh số liệu người chơi và thế giới ảo toàn cầu.
- `<address>` & `<footer>`: Thông tin công ty COGNOSPHERE PTE. LTD., bản quyền và liên kết mạng xã hội.
- **Không lạm dụng thẻ `<div>` vô nghĩa.**

### 2. Kỹ thuật CSS & CSS Variables
- **CSS Variables (`:root`)**: Quản lý bảng màu HoYoverse (`--primary-color`, `--secondary-color`, `--bg-main`, `--bg-card`, `--border-glow`), typography (`--font-heading`, `--font-body`), khoảng cách và bo góc nhất quán.
- **Bố cục hiện đại**: 
  - **CSS Grid**: Tự co giãn linh hoạt (`repeat(auto-fit, minmax(...))`) cho danh sách game và tin tức.
  - **CSS Flexbox**: Căn chỉnh Header, Nav, Hero CTA, Card Footer, Stats Banner.
- **Responsive Web Design**: Hoàn chỉnh trên Desktop, Tablet (≤1024px) và Mobile (≤768px). Menu di động hoạt động mượt mà bằng Pure CSS (Checkbox hack).

### 3. Tương tác & Thư viện (Libraries)
- **Animate.css**: Hiệu ứng chuyển động xuất hiện mượt mà cho tiêu đề Hero, huy hiệu và nút bấm chính.
- **AOS (Animate On Scroll)**: Hiệu ứng cuộn trang sinh động (`data-aos="fade-up"`, `data-aos="zoom-in"`, `data-aos-delay`) trên từng section và thẻ nội dung.
- **Hiệu ứng `:hover`, `:focus` tự viết bằng CSS thuần**: Nâng card khi rê chuột, phát sáng viền neon, zoom nhẹ thumbnail, viền focus ring rõ nét đạt chuẩn tiếp cận người dùng (Accessibility).

---

## 📁 Cấu Trúc Repository

```text
Duy_LeNhat_125000335/
├── assets/
│   └── images/
│       ├── hoyoverse-logo.svg
│       ├── genshin.jpg
│       ├── starrail.png
│       ├── zzz.jpg
│       ├── themis.jpg
│       └── honkai3rd.png
├── index.html
├── style.css
├── PROMPT_LOG.md
└── README.md
```

---

## 📝 Nhật Ký Vibe Coding
Xem chi tiết quá trình tương tác, ra lệnh và tinh chỉnh mã nguồn cùng AI tại: **[PROMPT_LOG.md](./PROMPT_LOG.md)**.
