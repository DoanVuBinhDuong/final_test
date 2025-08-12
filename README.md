Liệt kê và mô tả ngắn 2 phương pháp bảo mật API phổ biến.
*API Key
-Mô tả: Mỗi client khi gọi API sẽ phải gửi kèm một chuỗi khóa bí mật (API Key) được cấp trước. Server sẽ kiểm tra khóa này để xác thực quyền truy cập.
-Ưu điểm: Dễ triển khai, nhanh gọn.
-Nhược điểm: Không mã hóa dữ liệu, dễ bị lộ nếu client lưu trữ không an toàn.
*JWT (JSON Web Token)
-Mô tả: Khi đăng nhập thành công, server tạo một token dạng JSON được mã hóa (thường dùng HMAC hoặc RSA) và gửi cho client. Client sẽ gửi token này trong header mỗi lần gọi API để chứng thực.
-Ưu điểm: Bảo mật hơn API Key, có thể chứa thông tin người dùng, hết hạn theo thời gian.
-Nhược điểm: Token bị lộ trong thời gian còn hiệu lực thì có thể bị lợi dụng.

# Library API

## Mô tả
API quản lý thư viện cho phép quản lý người dùng, sách, danh mục, mượn/trả sách và xác thực OTP qua email. Hệ thống hỗ trợ phân quyền, xác thực JWT, kiểm tra dữ liệu đầu vào và tài liệu hóa API với Swagger.

## Tính năng chính
- Đăng ký, xác thực OTP, đăng nhập người dùng
- Quản lý sách (CRUD, phân trang)
- Quản lý danh mục sách (CRUD)
- Quản lý mượn/trả sách, báo cáo sách đang mượn
- Phân quyền người dùng (admin, user)
- Xác thực JWT cho các API bảo vệ
- Gửi email OTP xác thực tài khoản
- Kiểm tra dữ liệu đầu vào với Joi
- Tài liệu hóa API với Swagger UI

## Công nghệ sử dụng
- Node.js, Express.js
- MongoDB, Mongoose
- TypeScript
- JWT, Bcrypt
- Nodemailer
- Joi, express-validator
- Swagger UI

## Cài đặt
1. Cài đặt dependencies:
   ```bash
   npm install
   ```
2. Tạo file `.env` với nội dung mẫu:
   ```env
   MONGODB_URI=mongodb://localhost:27017/library
   EMAIL_USER=your_gmail@gmail.com
   EMAIL_PASS=your_gmail_app_password
   JWT_SECRET=your_jwt_secret
   PORT=3000
   ```

## Chạy ứng dụng
- Chạy ở chế độ phát triển:
  ```bash
  npm run dev
  ```
- Build và chạy production:
  ```bash
  npm run build
  npm start
  ```

## Tài liệu API
- Truy cập Swagger UI tại: [http://localhost:3000/api-docs](http://localhost:3000/api-docs)

## Ví dụ API
### Đăng ký người dùng
```
POST /users
{
  "name": "Nguyen Van A",
  "email": "a@gmail.com",
  "password": "123456",
  "role": "user"
}
```

### Đăng nhập
```
POST /auth/login
{
  "email": "a@gmail.com",
  "password": "123456"
}
```

### Gửi và xác thực OTP
```
POST /users/{id}/send-otp
POST /users/{id}/verify-otp
```

### Quản lý sách, danh mục, mượn trả
- Xem chi tiết tại Swagger UI hoặc các route `/books`, `/categories`, `/borrows`

## Đóng góp
Mọi đóng góp, báo lỗi hoặc đề xuất vui lòng tạo issue hoặc merge request.

## License
MIT 