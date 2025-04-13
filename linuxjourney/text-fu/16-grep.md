# 16. grep
Lệnh `grep` có thể sẽ là lệnh bạn sẽ dùng nhiều nhất khi cần xử lý văn bản 🐧.

:bulb: Lệnh này sẽ giúp bạn tìm kiếm file dựa theo một mẫu nhất định.

:bulb: Ngoài ra, lệnh này cũng giúp cho bạn biết liệu một file có tồn tại bên trong một thư mục hay nếu một chuỗi có tồn tại bên trong một file.

Giả sử chúng ta sử dụng lệnh với file sample.txt để thử nghiệm:

```sh
$ grep fox sample.txt
```

Lệnh trên sẽ tìm kiếm nội dung có chứa từ fox bên trong file sample.txt

Bạn cũng có thể tìm kiếm theo mẫu bỉ qua điều kiện chữ in hoa với flag `-i` (insensitive):

```sh
$ grep -i somepattern somefile
```

Để có thể tùy chỉnh phức tạp hơn, bạn có thể sử dụng `grep` kết hợp với toán tử `|`

```sh
$ env | grep -i User
```

😉 Dễ dàng nhận thấy, lệnh `grep` rất linh hoạt, chúng ta thậm chí có thể sử dụng biểu thức chính quy trong mẫu tìm kiếm như sau:

```sh
$ ls /somedir | grep '.txt$'
```

:bulb: Lệnh này sẽ trả ra toàn bộ các file kết thúc bằng đuôi .txt trong thư mục somedir.