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


## Google Drive (bản đăng nhập và đồng bộ)

Bản `index.html` đã tích hợp nút **☁️ Tài khoản** trên thanh đầu và **☁️ Google Drive** trong tab Ôn tập SRS.

1. Bảo đảm Google Drive API đã bật trong dự án Google Cloud.
2. Trong Google Auth Platform, tạo **OAuth Client ID** loại **Web application** với JavaScript origin `https://lehonghai25112005-wq.github.io` (không thêm `/HSK3.0/`).
3. Tại Audience, thêm email học thử vào **Test users** nếu ứng dụng đang ở Testing.
4. Tại Data Access, khai báo scope `https://www.googleapis.com/auth/drive.appdata`.
5. Triển khai lại `index.html` lên `main` của repository GitHub Pages. Mở website, bấm **Tài khoản → Đăng nhập Google**.
6. Lần đầu chọn **Lưu lên Drive** để đẩy tiến độ máy hiện tại lên, hoặc **Khôi phục từ Drive** nếu Drive đã có tiến độ. Không bấm lưu đè khi chưa chắc dữ liệu nào mới nhất. Sau đồng bộ thủ công lần đầu có thể bật tự động sao lưu.

* Lưu tiến độ trong Google Drive App Data Folder (không hiển thị trong danh sách file Drive thông thường).
* Không đưa **Client Secret**, mật khẩu hoặc token OAuth vào repository. OAuth Client ID là thông tin công khai của ứng dụng web.
* Đăng nhập Google cần Internet và một trang HTTPS đã khai báo origin. Chế độ học offline và sao lưu JSON cũ vẫn hoạt động.
* Client Secret cũ từng hiển thị trên ảnh chụp màn hình: nên xoay vòng/revoke trên Google Cloud và không gửi lại.
* Google OAuth ở Testing có thể yêu cầu đăng nhập lại khi phiên hết hạn; người dùng không phải đăng nhập liên tục khi chỉ học ngoại tuyến.
