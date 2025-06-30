```
it-company-portal/
├── Dockerfile                   # Docker setup cho app Node.js
├── docker-compose.yml           # Dịch vụ web + MongoDB + bot (nếu cần)
├── .env                         # Biến môi trường
├── .gitignore
├── README.md

├── src/
│   ├── app.js                   # Cấu hình Express middleware, routes
│   ├── server.js                # Điểm khởi động server (listen)

│   ├── config/
│   │   ├── db.js                # Kết nối MongoDB
│   │   └── roles.js             # Danh sách role trong hệ thống (admin, staff)

│   ├── routes/
│   │   ├── auth.js              # Đăng ký, đăng nhập
│   │   ├── admin.js             # Tất cả route dành riêng cho admin
│   │   ├── staff.js             # Route dành cho staff
│   │   └── index.js             # Tập hợp & mount tất cả routes chính

│   ├── controllers/
│   │   ├── authController.js        # Xử lý đăng ký, đăng nhập
│   │   ├── adminController.js       # Tất cả logic xử lý phía admin
│   │   ├── staffController.js       # Logic xử lý phía staff
│   │   └── supportController.js     # Gửi và xử lý support request (trigger XSS tại đây)

│   ├── middleware/
│   │   ├── auth.js              # Kiểm tra JWT, xác thực người dùng
│   │   └── roleCheck.js         # Kiểm tra quyền truy cập theo role

│   ├── models/
│   │   ├── User.js              # Thông tin người dùng (username, password, role)
│   │   ├── Task.js              # Task giao việc cho nhân viên
│   │   ├── Announcement.js      # Thông báo nội bộ
│   │   ├── Schedule.js          # Lịch làm việc của staff
│   │   ├── SupportRequest.js    # Support từ staff (có thể chứa XSS payload)
│   │   └── Rule.js              # Metadata của file nội quy upload (rule title, filename, etc.)

│   ├── views/
│   │   ├── login.html               # Trang đăng nhập
│   │   ├── dashboard.html           # Dashboard dùng chung sau login
│   │
│   │   ├── staff/
│   │   │   ├── schedule.html        # Lịch làm việc
│   │   │   ├── announcement.html    # Hiển thị thông báo từ admin
│   │   │   ├── support.html         # Gửi support (form chứa XSS input)
│   │   │   └── rules.html           # Trang xem file nội quy
│   │
│   │   └── admin/
│   │       ├── uploadCA.html        # Upload chứng chỉ CA
│   │       ├── viewCA.html          # Xem nội dung CA đã upload
│   │       ├── requests.html        # Xem support request từ staff (**bot truy cập để trigger XSS**)
│   │       ├── announcements.html   # Tạo mới thông báo cho công ty
│   │       └── uploadRule.html      # Upload file nội quy

│   └── utils/
│       ├── caUploader.js            # Xử lý upload file .crt/.pem (CA)
│       ├── ruleUploader.js          # Xử lý upload nội quy (PDF/HTML)
│       └── botTrigger.js            # Gửi yêu cầu đến `requests.html` bằng bot (puppeteer)

├── certs/
│   └── uploaded/
│       └── ca/                      # Lưu chứng chỉ CA do admin upload

├── public/
│   ├── css/                     # Các file CSS (Bootstrap/custom)
│   │   └── style.css
│   │
│   ├── js/                      # Các script frontend
│   │   └── main.js
│   │
│   ├── img/                     # Hình ảnh UI nếu có
│   │   └── logo.png
│   │
│   ├── rules/                   # File nội quy upload từ admin
│   │   └── rule_2025.pdf

├── scripts/
│   └── admin_bot.js                # Puppeteer headless bot (giả lập truy cập `requests.html` để trigger XSS)

```
