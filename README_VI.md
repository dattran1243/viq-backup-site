# VIQ Backup — Website cho Google OAuth Branding

**Gói này là website tĩnh riêng biệt, không phải source code của VIQ-Full.** Không dùng tài khoản Google Drive hay chạy Docker khi xem thử website.

## Các file

- `index.html`: trang giới thiệu chức năng và lý do xin quyền Google Drive.
- `privacy.html`: Privacy Policy mô tả `drive.file`, token, mã hóa, lưu trữ, chia sẻ, quyền xóa.
- `terms.html`: Terms of Service.
- `assets/site.css`, `assets/favicon.svg`: giao diện, không tải thư viện bên ngoài.
- `.nojekyll`: GitHub Pages không cần Jekyll.

## Bước 1 — Đổi email liên hệ trước khi công khai

Mở **`privacy.html` và `terms.html`**, thay tất cả chuỗi **`CONTACT_EMAIL_HERE`** bằng địa chỉ email bạn chấp nhận công khai. Nên dùng một email hỗ trợ riêng nếu không muốn lộ email cá nhân. Chọn email có người kiểm tra thường xuyên, phù hợp với email support trong Google OAuth Branding. **Không được xuất bản khi còn placeholder này.**

Không thêm Client Secret, access/refresh token, `rclone.conf`, khóa `viqcrypt`, ảnh màn hình chứa secret, hoặc file dữ liệu backup vào repo.

## Bước 2 — Xem thử ở Windows

Giải nén vào thư mục riêng, rồi nháy đúp `index.html` (Edge/Chrome). Nhấn Privacy và Terms để xem trang liên kết; có thể thu nhỏ trình duyệt kiểm tra giao diện điện thoại.

## Bước 3 — Đăng website bằng GitHub Pages (không upload project VIQ-Full)

1. Vào https://github.com/new, tạo repository tên `viq-backup-site`. Chọn **Public** nếu dùng GitHub Free. **KHÔNG** dùng repo VIQ-Full hiện có.
2. Trong repo mới, chọn **Add file > Upload files**, tải lên các file **bên trong thư mục** của gói này (giữ thư mục `assets/`), không phải chính thư mục bên ngoài. Có thể tải file ZIP lên GitHub bằng giao diện web nhưng GitHub sẽ lưu nguyên file ZIP, **không tự giải nén**; cần upload các file đã giải nén.
3. Commit changes. Vào **Settings > Pages**, **Build and deployment: Deploy from a branch**, chọn branch `main`, folder `/(root)`, rồi Save.
4. URL thường có dạng: `https://USERNAME.github.io/viq-backup-site/`. Đợi site được xuất bản, mở trình duyệt ẩn danh và thử cả 3 trang. Đây là **địa chỉ mẫu**; thay `USERNAME` bằng username thực tế.

Các link dùng đường dẫn tương đối, chạy được cả dưới `/viq-backup-site/` và khi bạn chuyển sang custom domain.

## Bước 4 — Quyền sở hữu tên miền và Google Cloud Branding

**Lưu ý quan trọng:** Google yêu cầu URL thuộc tên miền bạn có thể xác minh sở hữu qua Google Search Console. GitHub Pages miễn phí có URL dưới tên miền `github.io` dùng chung. Việc website chạy được không đảm bảo Google OAuth sẽ chấp nhận domain trong `Authorized domains`/brand verification. Nếu không xác minh được `USERNAME.github.io`, bạn sẽ cần **custom domain do bạn quản lý** (ví dụ `backup.example.com`), cấu hình nó cho GitHub Pages, và xác minh quyền sở hữu qua Search Console (DNS TXT hoặc cách Google hỗ trợ). Không nên cố nhập `github.io` như thể bạn sở hữu tên miền đó.

Google Cloud Console > Google Auth Platform > Branding:

- `Application home page`: URL HTTPS của trang chính, thí dụ `https://backup.example.com/` hoặc site Pages khi **được Google chấp nhận và đã xác minh**.
- `Application privacy policy link`: cùng tên miền + `/privacy.html`.
- `Application terms of service link`: cùng tên miền + `/terms.html`.
- `Authorized domains`: tên miền **thực tế bạn kiểm soát** và đã được Google chấp nhận; không thêm `https://`, path, hoặc tên miền của người khác.
- Logo: để trống; chỉ bổ sung nếu bạn muốn/đáp ứng yêu cầu xác minh.

Khi Branding được chấp nhận, sang Audience xem `Publish app` có hoạt động chưa. **Không bảo đảm Google sẽ bật Publish chỉ nhờ tạo website**; Google có thể yêu cầu bước xác minh/giải trình khác.

## Bước 5 — OAuth và dữ liệu nhạy cảm

- Nếu Google OAuth vẫn `Testing`, token cho ứng dụng External thường có giới hạn thời gian, cần lên kế hoạch cấp quyền lại.
- Trước khi làm backup lớn, xác nhận Client Secret từng lộ đã được xoay vòng/thu hồi và rclone đang dùng secret mới.
- Bảo đảm khóa `viqcrypt` và cấu hình giải mã đã có bản dự phòng độc lập, an toàn.
- Website chỉ là trang giới thiệu. **Nó không sao lưu dữ liệu và không thay đổi Docker/WSL.**

## Nguồn tài liệu

- Google OAuth branding: https://support.google.com/cloud/answer/15549049?hl=en
- Google OAuth production policies: https://developers.google.com/identity/protocols/oauth2/policies
- Google Search Console verification: https://support.google.com/webmasters/answer/9008080?hl=en
- GitHub Pages: https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site
- rclone `drive.file`: https://rclone.org/drive/

**Rà soát nội dung Privacy Policy và Terms để khớp hoạt động thực tế trước khi đưa lên public.** Đây là bản thảo dựa trên quy trình VIQ Backup hiện tại, không phải chứng nhận Google đã chấp thuận hoặc tư vấn pháp lý.
