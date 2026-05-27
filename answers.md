# PBT_06 - CSS Frameworks

Họ tên: Trịnh Bùi Duy Nguyên

Email: nguyentwd.hubt@gmail.com


Track đã chọn: Bootstrap 5

## Phần A - Đọc hiểu

### Câu A1 - Grid System

| Kích thước | < 768px | 768px - 991px | ≥ 992px |
|---|---|---|---|
| Số cột | 1 cột mỗi box | 2 cột mỗi box | 4 cột mỗi box |
| Box layout | Mỗi box chiếm 100% chiều ngang, xếp dọc 4 hàng | Box 1-2 ở hàng 1, Box 3-4 ở hàng 2 | 4 box nằm trên 1 hàng |

Giải thích: `col-12` dùng cho mobile, `col-md-6` cho tablet, `col-lg-3` cho desktop lớn.

`col-md-6` nghĩa là từ breakpoint `md` trở lên, phần tử chiếm 6/12 cột, tức 50% chiều rộng hàng.

Không cần viết `col-sm-12` vì Bootstrap là mobile-first. Nếu không khai báo gì cho màn hình nhỏ hơn `md`, phần tử sẽ tự động xếp theo chiều rộng đầy đủ của cột cha, nên `col-12` thường đã đủ cho mobile.

### Câu A2 - Utilities & Components

1. `d-none d-md-block` nghĩa là ẩn ở mọi kích thước mặc định, và chỉ hiển thị dạng block từ `md` trở lên. Tức là ẩn trên mobile, hiện trên tablet và desktop.

2. 5 spacing utilities:
   - `mt-3` → margin-top: 1rem
   - `px-4` → padding-left và padding-right: 1.5rem
   - `mb-auto` → margin-bottom tự động, thường dùng trong flex layout để đẩy phần tử xuống dưới
   - `mx-2` → margin trái phải: 0.5rem
   - `py-5` → padding trên dưới: 3rem

3. Khác nhau giữa `.container`, `.container-fluid`, `.container-md`:
   - `.container` → có max-width theo breakpoint, căn giữa trang, thường dùng cho nội dung chính.
   - `.container-fluid` → luôn full-width 100%, thường dùng cho hero, footer, section nền rộng.
   - `.container-md` → full-width dưới `md`, nhưng từ `md` trở lên sẽ có max-width như container.

## Phần C - Phân tích

### Câu C1 - Tùy biến Bootstrap

1. Muốn đổi màu `$primary` sang `#E63946` thì cần dùng Bootstrap source SASS, cài `bootstrap` và `sass` qua npm, sau đó tạo file SCSS riêng như `custom.scss`. Trong file này phải override `$primary: #E63946;` trước khi `@import "bootstrap/scss/bootstrap";`. Sau đó chạy compiler như `sass src/custom.scss dist/style.css` để build CSS mới.

2. Không nên override trực tiếp `.btn-primary { background: red; }` vì đó là sửa bề mặt, dễ lệch trạng thái hover/focus/active và phải tự sửa nhiều component liên quan. Dùng SASS variables tốt hơn vì Bootstrap sẽ sinh toàn bộ hệ thống màu nhất quán từ một nguồn, giúp đồng bộ giữa button, badge, alert, link, utilities và dễ bảo trì.

### Câu C2 - So sánh

Ví dụ CSS thuần cho một navbar responsive và một product card:

```css
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 24px;
  background: #111827;
  color: #fff;
}

.nav-links {
  display: flex;
  gap: 24px;
}

.nav-toggle {
  display: none;
}

.product-card {
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08);
}

.product-card img {
  width: 100%;
  display: block;
}

.product-card .body {
  padding: 16px;
}

@media (max-width: 991px) {
  .nav-links {
    display: none;
  }
  .nav-toggle {
    display: inline-flex;
  }
}
```

So sánh với Bootstrap version:
- Số dòng CSS cần viết: CSS thuần thường nhiều hơn vì phải tự viết layout, responsive, states và spacing. Bootstrap chỉ cần ghép class.
- Thời gian phát triển: Bootstrap nhanh hơn rõ rệt vì có sẵn component và utilities.
- Khả năng tùy biến: CSS thuần linh hoạt cao nhất; Bootstrap linh hoạt tốt nhưng có khung sẵn và dễ đồng bộ hơn.
- Nên dùng Bootstrap khi cần làm nhanh, dashboard, internal tool, prototype, hoặc team muốn thống nhất UI.
- Không nên dùng Bootstrap khi cần thiết kế cực kỳ độc quyền, tối ưu bundle thật sâu, hoặc đã có design system riêng và muốn kiểm soát tuyệt đối từng pixel.
