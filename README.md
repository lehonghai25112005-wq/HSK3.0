# HSK 3.0 · Bộ học tiếng Trung trên GitHub Pages

Bản website tĩnh được đóng gói từ file học HSK 3.0 (bản giao diện rộng, Gấu trúc & Trúc xanh).

## Hướng dẫn xuất bản HTTPS

1. Đăng nhập [GitHub](https://github.com/) và tạo repository mới, ví dụ `hsk30` (để **Public** nếu dùng GitHub Free).
2. Tại repository, chọn **Add file → Upload files** rồi tải các tệp `index.html` và `.nojekyll` lên ở **thư mục gốc**; chọn **Commit changes**. Bạn cũng có thể tải nội dung ZIP lên sau khi giải nén.
3. Mở **Settings → Pages**.
4. Ở **Build and deployment → Source**, chọn **Deploy from a branch**. Chọn nhánh `main`, thư mục `/(root)`, rồi **Save**.
5. Mở địa chỉ `https://TEN-TAI-KHOAN.github.io/hsk30/` (thay tên tài khoản và tên repository thực tế). GitHub sẽ hiển thị URL chính xác ở mục Pages sau khi triển khai thành công.

Nếu repository tên là `TEN-TAI-KHOAN.github.io`, địa chỉ sẽ là `https://TEN-TAI-KHOAN.github.io/`.

## Giữ tiến độ khi chuyển từ file HTML sang website

Trình duyệt xem file `file://` và địa chỉ `https://` là hai vùng lưu tiến độ khác nhau. Hãy mở file học cũ, vào **Ôn tập SRS** rồi chọn **Sao lưu toàn bộ tiến độ (.json)**. Khi website đã mở được, vào **Ôn tập SRS → Khôi phục tiến độ** và chọn file JSON đó.

- Không đưa file JSON sao lưu lên GitHub. Nếu repository là công khai, người khác có thể đọc những tệp được đẩy lên đó.
- File này tự lưu tiến độ vào bộ nhớ trình duyệt; **chưa có đăng nhập hoặc đồng bộ Google Drive thực sự**. Việc có HTTPS chỉ là bước đầu để sau này cấu hình Google OAuth và Drive API.
- Một số chức năng tùy chọn như hướng dẫn thứ tự nét động cần Internet.

## Khi triển khai đăng nhập Google trong bước tiếp theo

Cần tạo Google Cloud Project, bật Google Drive API và tạo OAuth Client ID cho ứng dụng web. JavaScript origin là `https://TEN-TAI-KHOAN.github.io` (chỉ origin, không gồm `/hsk30/`). Đăng nhập / đồng bộ không hoạt động cho đến khi OAuth được cấu hình và tích hợp vào website.

> Không đưa Client Secret, access token, mật khẩu hay bản sao lưu tiến độ riêng tư vào GitHub. OAuth Client ID (không phải Client Secret) là thông tin định danh ứng dụng ở phía trình duyệt.

Tài liệu chính thức:
- https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
- https://developers.google.com/workspace/drive/api/quickstart/js
