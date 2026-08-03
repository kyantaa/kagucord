# Hướng dẫn triển khai

Gói này thay thế `index.html` cũ (16MB, ảnh nhúng cứng trong code) bằng một
website tĩnh gọn nhẹ, đọc toàn bộ nội dung từ `data.json`, kèm một trang quản
trị (`admin.html`) để bạn tự sửa nội dung/ảnh/nhạc mà **không cần đụng code**.

## 1. Các file trong gói

| File / thư mục     | Vai trò                                                        |
|---------------------|-----------------------------------------------------------------|
| `index.html`         | Trang web chính (đã gọn còn ~28KB, tự tải `data.json` để hiển thị) |
| `data.json`           | Toàn bộ nội dung văn bản + đường dẫn ảnh/nhạc                    |
| `admin.html`          | Trang quản trị — sửa nội dung rồi lưu thẳng lên GitHub          |
| `assets/avatar/`      | Ảnh đại diện                                                    |
| `assets/gallery/`     | Ảnh trong mục "Thiết kế Banner"                                 |
| `assets/sites/`       | Ảnh xem trước các trang web đã làm                              |
| `icon.png`, `nhac-nen.mp3` | Favicon và nhạc nền (giữ nguyên từ repo cũ)                |

## 2. Đưa lên GitHub (làm 1 lần)

1. Vào repo `https://github.com/kyantaa/kagucord`, nhánh **root**.
2. **Xoá** `index.html` cũ (bản 16MB), giữ lại hoặc xoá `bg.jpg` tuỳ bạn (file này
   không được index.html dùng tới).
3. Kéo-thả (drag & drop) toàn bộ nội dung trong gói này (`index.html`,
   `data.json`, `admin.html`, thư mục `assets/`, `icon.png`, `nhac-nen.mp3`)
   vào giao diện web GitHub ("Add file" → "Upload files"), rồi bấm **Commit
   changes** trực tiếp vào nhánh `root`.
   - Có thể làm bằng `git` dòng lệnh nếu bạn quen thuộc hơn.

Sau bước này, trang web (`index.html`) sẽ chạy y hệt như cũ nhưng nhẹ hơn rất
nhiều và không còn ảnh nhúng cứng trong code nữa.

## 3. Tạo GitHub token để dùng trang quản trị

1. Vào **github.com/settings/tokens?type=beta** → **Generate new token**.
2. Đặt tên bất kỳ, chọn **Only select repositories** → chọn repo `kagucord`.
3. Ở phần **Repository permissions**, chọn **Contents: Read and write**.
4. Generate token, copy lại chuỗi bắt đầu bằng `github_pat_...`.
   (Token dạng cũ `ghp_...` cũng dùng được nếu bạn quen tạo kiểu đó — nhớ cấp
   quyền `repo`.)

⚠️ Token có quyền ghi vào repo của bạn — không chia sẻ cho ai, không dùng trên
máy tính công cộng nếu không bấm "Quên token" sau khi dùng xong.

## 4. Dùng trang quản trị

1. Mở `https://kyantaa.github.io/kagucord/admin.html` (hoặc đường dẫn tương
   ứng nơi bạn host trang, ví dụ `kyantane.io.vn/admin.html`).
2. Điền **owner** = `kyantaa`, **repo** = `kagucord`, **branch** = `root`,
   dán **token** vào, bấm **Kết nối & tải nội dung**.
3. Sửa các trường (tên, giới thiệu, thẻ, ảnh đại diện, nhạc nền, danh sách
   thiết kế/trang web/dự án/máy chủ/mạng xã hội...). Có thể **Thêm mục mới**
   hoặc **Xoá** từng mục.
4. Khi xong, bấm **💾 Lưu & xuất bản** ở thanh dưới cùng. Trang quản trị sẽ tự
   tải ảnh/nhạc mới lên thư mục `assets/` tương ứng và cập nhật `data.json`
   trực tiếp trên GitHub — web tĩnh (`index.html`) sẽ hiển thị nội dung mới
   sau khi trang deploy lại (thường vài chục giây tới vài phút nếu bạn dùng
   GitHub Pages).

Toàn bộ web (`index.html`) vẫn là file tĩnh thuần HTML/CSS/JS — không có máy
chủ, không có database. `admin.html` chỉ là một trang tĩnh khác gọi thẳng tới
GitHub API bằng token của bạn để "commit" thay đổi, nên bạn không cần đụng gì
tới code khi muốn cập nhật nội dung.

## 5. Ghi chú thêm

- Nếu muốn giấu `admin.html` khỏi công cụ tìm kiếm, có thể thêm dòng
  `Disallow: /admin.html` vào file `robots.txt` của repo.
- Nếu muốn bảo mật hơn nữa, có thể đặt tên file khác cho `admin.html`
  (ví dụ `quantri-bimat.html`) để người lạ khó đoán ra đường dẫn.
- File `data.json` bạn hoàn toàn có thể tự mở và sửa tay trên GitHub (bấm
  bút chì ✏️ ở trang GitHub) nếu không muốn dùng trang quản trị.
