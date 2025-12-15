Như bài santa's shop thường ta vẫn sẽ đăng nhập vào web như bình thường, nhưng mục tiêu bài này ta sẽ cần phải mua được Mystery Gift Box - Nơi chứa flag

Bài đã gợi ý ta chỉ có thể nạp coin từ localhost

<img width="508" height="153" alt="image" src="https://github.com/user-attachments/assets/108125f3-9c6d-4dd8-8564-11638f9cc1a9" />

nên ta sẽ dùng phương pháp SSRF để ép server tự gọi vào trang admin với tư cách là admin để nạp coin cho mình.
Nhưng ta không thể dùng cách thông thường là thay đổi cookie được, để làm thế ta cần phải vượt qua lớp bảo mật admin mà cách này phải thông qua 2 điều kiện:
1. dùng cookie admin ( như đã nói ko thể thay đổi )
2. Secret key, server check tham số secret=KEY trong url.

Ta sẽ tập trung vào điều kiện thứ 2. Lấy key bằng LFI, cần đọc nội dung file /secrect.txt
Truy cập vào url sau: view-source:http://67.223.119.69:5027/file.php?image=php://filter/convert.base64-encode/resource=/secret.txt

Khi truy cập vào link ta sẽ thấy 1 chuỗi base64, copy và decode nó sẽ ra được secret key

<img width="488" height="478" alt="image" src="https://github.com/user-attachments/assets/d318b384-0201-423b-8253-8fc81f181eac" />

*Giải thích đoạn này 1 chút tại sao ta cần phải encode sang base64. Vì trong các loại file như secret sẽ có thể chứa các kí tự đặc biệt như <, >, /. Có thể khiến web tưởng đây là code HTML nên sẽ thực thi nó.
Để tránh điều này ta sẽ encode sang base64 rồi decode ngược lại thì sẽ an toàn hơn. OK?🧐

Tiếp theo sẽ áp dụng SSRF
Payload: http://67.223.119.69:5027/file.php?image=http://127.0.0.1/admin.php?username=TH%26coin= 36363636%26secret=ChiCon1BuocNuaThoi~_~

*Đoạn này mình nhờ Gemini nó tạo payload hộ nên k biết giải thích sao 🐧, đại loại là n sẽ bắn SSRF qua LFI, với số tiền mong muốn*

<img width="975" height="419" alt="image" src="https://github.com/user-attachments/assets/739083e5-4f7b-4d35-8d37-cf7e087837f3" />

Reload trang là ta sẽ có tiền và lấy Gift thoi
