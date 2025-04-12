# 6. cut

Chúng ta sẽ bắt đầu tìm hiểu một số lệnh hữu ích để thao tác với text. Trước khi bắt đầu thì cần chuẩn bị một file có nội dung để thao tác, sao chép rồi dán lệnh sau, lưu ý là có một kí tự tab giữa chữ "lazy" và "dog":

```sh
$ echo 'The quick brown; fox jumps over the lazy  dog' > sample.txt
```

:bulb: Lệnh đầu tiên mà chúng ta sẽ tìm hiểu là lệnh `cut`. Nó sẽ tách các phần văn bản từ một file.

Giả sử, để tách nội dung theo kí tự:

```sh
$ cut -c 5 sample.txt
```

:point_right: Lệnh này tách kí tự thứ 5 của mỗi dòng trong một file. Trong trường hợp này là kí tự "q". :boom: Lưu ý là khoảng trắng cũng được tính là một kí tự.

Để trích xuất nội dung theo một trường nhất định nào đó, chúng ta cần sửa đổi lệnh lại một chút:

```sh
$ cut -f 2 sample.txt
```

flag `-f` viết tắt cho `field` chỉ ra rằng nên cắt văn bản dựa theo trường, mặc định thì nó sẽ dùng TABs để làm kí tự phân cách, thế nên tất cả mọi thứ tách biệt với nhau bởi kí tự TAB được xem như là một trường.

:point_right: Trong trường hợp này, lệnh trên sẽ trả ra chữ "dog". Vì chữ dog là thành phần thứ 2 được phân tách bởi kí tự TAB.

Bạn có thể kết hợp field flag với delimeter flag `-d` để có thể phân tách nội dung dựa vào một kí tự mà chúng ta tự định nghĩa:

```
$ cut -f 1 -d ";" sample.txt
```

:point_right: Lệnh này sẽ phân tách nội dung dựa vào kí tự `;`, tức là mọi thành phần cách nhau bởi dấu ; sẽ được xem như là một field riêng biệt, và lệnh này sẽ lấy ra field đầu tiên, tức là "quick brown".