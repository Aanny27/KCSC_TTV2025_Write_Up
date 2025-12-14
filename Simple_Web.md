Bài này liên quan đến lỗi Unicode normalization (chuẩn hóa unicode). Nên ta ko thể đăng nhập với các kí tự bình thường được.
Ta cần đăng kí với tên tài khoản là ａdmin ( chữ a đầu là ký tự fullwidth ), mật khẩu để gì cũng được. Sau đó đăng nhập cùng với chữ "admin" bình thường là ta có thể vào trang web với quyển quản trị là admin

<img width="932" height="594" alt="image" src="https://github.com/user-attachments/assets/65c1517e-3d0c-4039-a138-b41a9673cfc5" />

Dựa vào ảnh ta có thể thấy Security Notice: You can only read /flag with local access, điều này nghĩa là ta cần yêu cầu server truy cập vào chính nó để đọc file /flag

Thử với http://localhost/flag thì không thu được gì. Quay trở lại với đề bài gợi ý đây là lỗi về unicode nên ta sẽ thử đổi kiểu kí tự

http://ⓛⓞⓒⓐⓛⓗⓞⓢⓣ/flag?a=1. Đoạn này thêm biến 1 vào vì đôi khi server cần tham số bừa để không cache.

<img width="716" height="401" alt="image" src="https://github.com/user-attachments/assets/a6c198c4-66fa-43e2-acaa-2a31201bd917" />
D0n3!!
