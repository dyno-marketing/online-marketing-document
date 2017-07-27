### Bước 1
Chèn đoạn script sau ở trong thẻ `<head>`

```html
<script src="http://smartpx.io/sdk/smartpx.min.js?v=1.0"></script>
```
### Bước 2
Để truy vấn các api thông tin người dùng, cần phải có session_id. Để lấy session_id thì lấy qua đoạn script sau

```html
<script>
var session_id = readCookie('smartpx_session_id');
</script>
```
