### Bước 1
Tạo 1 page để bạn có thể gửi messenger cho người dùng. Cấp quyền quản trị page cho Smartpx để có thể thêm vào chatbot

### Bước 2
Bạn cung cấp các tên miền (đầy đủ cả http/https) mà bạn muốn tracking người dùng cho Smartpx

### Bước 3
Sau khi Smartpx thêm các tên miền bạn gắn đoạn script này vào bất kỳ chỗ nào trên trang của bạn mà bạn muốn hiện nút "Bắt đầu"

`your_domain` là tên miền trang web mà bạn chèn đoạn script

`your_page_id` là id của page mà bạn đã cấp quyền

```html
<div id="started_button" origin="http://your_domain" page_id="your_page_id"></div>
<script src="http://smartpx.io/sdk.min.js"></script>
```
### Bước 4
Để truy vấn các api thông tin người dùng, cần phải có session_id. Để lấy session_id thì lấy qua đoạn script sau

```html
<script>
var session_id = readCookie('smartpx_session_id');
</script>
```
