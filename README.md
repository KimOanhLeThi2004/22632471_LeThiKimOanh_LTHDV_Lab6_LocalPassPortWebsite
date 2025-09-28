# Passport Authentication Project

Ứng dụng này triển khai hệ thống đăng ký, đăng nhập và profile bảo vệ bằng session sử dụng Node.js, Express, MongoDB và Passport.js. Hỗ trợ cả form x-www-form-urlencoded và JSON cho các request từ client hoặc Postman.

## Công nghệ sử dụng
Node.js, Express.js, MongoDB, Mongoose, Passport.js (Local Strategy), express-session và EJS làm view engine.

## Cấu trúc project
project/  
├─ models/  
│   └─ User.js          # Mongoose model user  
├─ routes/  
│   └─ auth.js          # Các route register, login, profile, logout  
├─ config/  
│   └─ passport.js      # Cấu hình passport local strategy  
├─ views/  
│   ├─ register.ejs  
│   ├─ login.ejs  
│   └─ profile.ejs  
├─ app.js               # File main server  
└─ package.json

## Cài đặt
1. Clone repo:  
git clone https://github.com/KimOanhLeThi2004/22632471_LeThiKimOanh_LTHDV_Lab6_LocalPassPortWebsite.git
2. Cài đặt dependencies:  
npm install
3. Khởi động MongoDB:  
- Windows: mở MongoDB service hoặc dùng mongod  
- Linux/Mac: mongod --dbpath <đường dẫn tới dữ liệu>  
4. Chạy server:  
node app.js
Server chạy tại: [http://localhost:3000](http://localhost:3000)

## Các route
- Register: GET `/register` hiển thị form đăng ký, POST `/register` tạo tài khoản mới với body x-www-form-urlencoded (`username`, `password`) hoặc JSON (`{"username": "testuser","password": "123456"}`)  
- Login: GET `/login` hiển thị form login, POST `/login` đăng nhập với body x-www-form-urlencoded hoặc JSON giống register  
- Profile: GET `/profile` là protected route hiển thị thông tin user chỉ khi session active  
- Logout: GET `/logout` để đăng xuất và redirect về `/login`

## Hướng dẫn test bằng Postman
### Hướng dẫn test bằng Postman
- POST [http://localhost:3000/register](http://localhost:3000/register) – gửi dữ liệu dạng x-www-form-urlencoded hoặc raw JSON, với x-www-form-urlencoded điền `username` và `password`, JSON ví dụ: `{"username": "testuser", "password": "123456"}`; thành công sẽ redirect sang [http://localhost:3000/login](http://localhost:3000/login) hoặc trả JSON `{ "message": "User created" }` nếu code hỗ trợ JSON.  
- POST [http://localhost:3000/login](http://localhost:3000/login) – gửi dữ liệu giống `/register`, thành công redirect [http://localhost:3000/profile](http://localhost:3000/profile), thất bại redirect [http://localhost:3000/login](http://localhost:3000/login) hoặc trả JSON `{ "message": "Invalid credentials" }`; bật Follow redirects và giữ cookie để truy cập `/profile`.  
- GET [http://localhost:3000/profile](http://localhost:3000/profile) – cần cookie session từ login; nếu đã login sẽ trả view hoặc JSON thông tin user, nếu chưa login sẽ redirect về [http://localhost:3000/login](http://localhost:3000/login).  
- GET [http://localhost:3000/logout](http://localhost:3000/logout) – đăng xuất, redirect về [http://localhost:3000/login](http://localhost:3000/login).

Lưu ý: Passport Local Strategy mặc định lấy `username` và `password` từ `req.body`, server hỗ trợ cả JSON và form x-www-form-urlencoded, password chưa được hash nên không nên dùng trong production. License: MIT.  

## Lưu ý
- Passport Local Strategy mặc định lấy `username` và `password` từ `req.body`  
- Server hỗ trợ cả JSON và form x-www-form-urlencoded  
- Password chưa được hash nên không nên dùng trong production

## License
MIT
