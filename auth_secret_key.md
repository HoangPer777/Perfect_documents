Hướng dẫn chi tiết từng bước:

1. GOOGLE_CLIENT_SECRET
Bước 1: Vào console.cloud.google.com → đăng nhập Google account

Bước 2: Chọn project đang dùng (hoặc tạo mới nếu chưa có)

Bước 3: Menu trái → "APIs & Services" → "Credentials"

Bước 4: Tìm OAuth 2.0 Client ID có client_id là 614152899483-... → click vào cái bút chì (edit)

Bước 5: Copy giá trị "Client secret" — trông như GOCSPX-xxxxxxxxxxxxxxxx

Bước 6: Trong phần "Authorized redirect URIs" → click "Add URI" → thêm:

http://localhost:8080/login/oauth2/code/google
→ Save

2. FACEBOOK_CLIENT_SECRET
Bước 1: Vào developers.facebook.com → My Apps → chọn app ID 1163485252397725

Bước 2: Menu trái → Settings → Basic

Bước 3: Click "Show" cạnh "App Secret" → nhập mật khẩu Facebook → copy chuỗi đó

Bước 4: Menu trái → Facebook Login → Settings → "Valid OAuth Redirect URIs" → thêm:

http://localhost:8080/login/oauth2/code/facebook
→ Save Changes

3. Gmail cho MAIL (dùng App Password — không cần mật khẩu Gmail thật)
Bước 1: Vào Gmail account bạn muốn dùng để gửi mail → myaccount.google.com

Bước 2: Security → "2-Step Verification" → bật lên nếu chưa bật (bắt buộc)

Bước 3: Sau khi bật 2FA → quay lại Security → tìm "App passwords" (hoặc vào thẳng myaccount.google.com/apppasswords)

Bước 4: App name: gõ PerfectMarket → click "Create"

Bước 5: Google sẽ hiện một mật khẩu 16 ký tự dạng xxxx xxxx xxxx xxxx → copy (bỏ dấu cách)

Bước 6: Điền vào .env:

MAIL_USERNAME=your-gmail@gmail.com
MAIL_PASSWORD=xxxxxxxxxxxxxxxx   ← 16 ký tự không có dấu cách