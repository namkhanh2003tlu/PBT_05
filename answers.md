# PHIẾU BÀI TẬP 05 — ĐÁP ÁN

## PHẦN A — KIỂM TRA ĐỌC HIỂU

### Câu A1 — Viewport & Mobile-First

1. Thẻ viewport chuẩn:
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
- `width=device-width`: đặt chiều rộng viewport bằng chiều rộng thiết bị.
- `initial-scale=1.0`: thiết lập tỷ lệ zoom ban đầu là 100%.

2. Nếu thiếu thẻ này, iPhone sẽ hiển thị trang ở chế độ desktop thu nhỏ, trang bị thu nhỏ về width lớn hơn, chữ và layout sẽ rất nhỏ và không responsive.

3. Mobile-First vs Desktop-First:
- Mobile-First: CSS mặc định cho mobile, sau đó dùng `@media (min-width: 768px)` để mở rộng cho tablet/desktop.
- Desktop-First: CSS mặc định cho desktop, dùng `@media (max-width: 768px)` để thu hẹp cho tablet/mobile.

Ví dụ Mobile-First:
```css
.container { width: 100%; }
@media (min-width: 768px) {
  .container { width: 720px; }
}
```
Ví dụ Desktop-First:
```css
.container { width: 720px; }
@media (max-width: 767px) {
  .container { width: 100%; }
}
```
Mobile-First được khuyên dùng vì nó ưu tiên thiết bị nhỏ, tối giản CSS ban đầu và phù hợp với progressive enhancement.

### Câu A2 — Breakpoints

Breakpoints chuẩn (theo Bootstrap):
- `576px` — Small (sm): điện thoại lớn, 1-2 cột.
- `768px` — Medium (md): tablet, 2 cột.
- `992px` — Large (lg): laptop nhỏ, 3 cột.
- `1200px` — Extra large (xl): desktop, 4 cột.
- `1400px` — Extra extra large (xxl): desktop rộng.

Ví dụ product grid:
- Mobile: 1 cột
- Tablet: 2 cột
- Desktop: 4 cột

### Câu A3 — Media Queries

| Chiều rộng màn hình | `.container` width |
|---------------------|--------------------|
| 375px | 100% |
| 600px | 540px |
| 800px | 720px |
| 1000px | 960px |
| 1400px | 1140px |

### Câu A4 — SCSS Basics

1. Variables: dùng để lưu giá trị lặp lại.
```scss
$primary-color: #2563eb;
```
2. Nesting: cho phép viết selector lồng nhau.
```scss
.card {
  .title { color: #111; }
}
```
3. Mixins: định nghĩa đoạn CSS tái sử dụng.
```scss
@mixin flex-center {
  display: flex;
  align-items: center;
  justify-content: center;
}
@include flex-center;
```
4. @extend / Inheritance: chia sẻ style giữa các selector.
```scss
.button { padding: 12px; }
.btn-primary { @extend .button; background: blue; }
```
Trình duyệt không đọc được file `.scss` vì nó là ngôn ngữ tiền xử lý. Cần biên dịch SCSS thành CSS bằng công cụ như `sass` hoặc `node-sass`.

## PHẦN B — THỰC HÀNH CODE

### Bài B1 — Responsive Product Page

File:
- `responsive.html`
- `responsive.css`

Yêu cầu đã thực hiện:
- Mobile-First: CSS mặc định cho mobile.
- Breakpoint tablet: `@media (min-width: 768px)`.
- Breakpoint desktop: `@media (min-width: 1024px)`.
- Ảnh responsive `max-width: 100%; height: auto;`.
- Font size thay đổi tại breakpoint.
- Navigation hamburger trên mobile và menu ngang trên desktop.
- Sidebar ẩn trên mobile.
- 8 product cards.

### Bài B2 — CSS Transitions & Animations

File:
- `animations.html`
- `animations.css`

Hiệu ứng:
- Card hover translate + shadow.
- Button hover đổi màu + scale.
- Image zoom trên hover.
- Spinner xoay vòng với `@keyframes spin`.
- Fade-in animation với `@keyframes fadeIn`.

### Bài B3 — SCSS Refactor

File:
- `scss/_variables.scss`
- `scss/_mixins.scss`
- `scss/_components.scss`
- `scss/style.scss`
- `style.css` (CSS đã biên dịch từ SCSS)

SCSS đã sử dụng:
- variables: 8 biến.
- nesting và parent selector `&`.
- mixins: `respond-to`, `flex-center`, `card-shadow`.
- partials + import: `variables`, `mixins`, `components`.

Lệnh biên dịch (nếu sass đã cài):
```bash
sass scss/style.scss style.css
```

> Trong môi trường hiện tại, `sass` không có sẵn, nên file `style.css` được tạo trực tiếp theo cấu trúc CSS tương tự SCSS biên dịch.

## PHẦN C — PHÂN TÍCH

### Câu C1 — Phân tích trang web thực

Mở một trang như Shopee, Tiki hoặc VNExpress ở 3 kích thước: mobile 375px, tablet 768px, desktop 1440px.
- Navigation trên mobile thường thành hamburger hoặc collapse vào menu.
- Lưới content thu nhỏ số cột từ 4-5 cột trên desktop xuống 2 cột tablet và 1 cột mobile.
- Một số filter/ads/ảnh được ẩn trên mobile.
- Font size thường nhỏ hơn trên mobile để vừa màn hình.

### Câu C2 — Thiết kế Responsive Strategy

Mobile:
- Header logo + điện thoại chạy trên cùng.
- Hero full width.
- Grid 6 ảnh 1 cột.
- Form đặt bàn dưới hero.
- Bản đồ hiển thị sau form.
- Sidebar ẩn.

Tablet:
- Grid ảnh 2 cột.
- Logo + số điện thoại vẫn ở header.
- Bản đồ nằm dưới form hoặc cạnh form nếu đủ rộng.

Desktop:
- Layout 3 cột: sidebar filter + content + bản đồ.
- Grid ảnh 3 cột.
- Form bên cạnh hero hoặc dưới hero tùy thiết kế.

CSS skeleton Mobile-First:
```css
.page {
  display: grid;
  gap: 16px;
}
.hero,
.form,
.gallery,
.map {
  width: 100%;
}

@media (min-width: 768px) {
  .gallery { grid-template-columns: repeat(2, 1fr); }
}

@media (min-width: 1024px) {
  .page {
    grid-template-columns: 1fr 1fr;
  }
  .sidebar {
    display: block;
  }
}
```

> Chụp screenshot responsive ở 3 breakpoints 375px, 768px, 1200px vào folder `screenshots/`.

## File PBT_05 đã tạo

- `responsive.html`
- `responsive.css`
- `animations.html`
- `animations.css`
- `scss/_variables.scss`
- `scss/_mixins.scss`
- `scss/_components.scss`
- `scss/style.scss`
- `style.css`
- `answers.md`

> Video OBS chưa tạo theo yêu cầu của bạn.
