# 5. env (Enviroment)

Chạy thử lệnh sau:

```sh
$ echo $HOME
```

Bạn sẽ thấy kết quả in ra màn hình là thư mục /home của người dùng hiện tại. 

Thử tiếp lệnh sau nhé

```sh
$ echo $USER 
```

Kết quả trả ra username của bạn. :confused: Khoan đã, $HOME, \$USER là cái quái gì thế, có phải là một lệnh không? 

Đùa thôi :unamused: tôi nghĩ đa số chúng ta đều đoán được đây là gì, đây là các biến có chứa giá trị bên trong nó.

Câu hỏi là các biến này nó đến từ đâu, về cơ bản đây là các biến môi trường. Bạn có thể xem chúng với lệnh:

```sh
$ env 
```

:bulb: Lệnh này sẽ trả ra rất nhiều thông tin về các biến môi trường đang được thiết lập cho người dùng hiện tại. Các biến này sẽ chứa một số thông tin hữu ích mà các tiến trình hoặc shell khác có thể sẽ dùng đến.

Đây là một ví dụ ngắn:

```sh
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/bin

PWD=/home/user

USER=pete
```

Có một loại biến đặc biệt mà bạn cần chú ý là biến PATH, bạn có thể in giá trị của một biến với toán tử `$` như sau:

```sh
$ echo $PATH

/usr/local/sbin:/usr/local/bin:/usr/sbin:/bin
```

:bulb: Lệnh này trả ra một danh sách các đườnh dẫn sẽ ngăn cách nhau bằng dấu `:`. Hệ thống sẽ tìm kiếm file thực thi cho các lệnh dựa vào các đường dẫn được liệt kê tại đây.

- :point_right: Giả sử, bạn tải một package lệnh mới từ internet về rồi đặt file thực thi ở thư mục nào đó không phải mặc định.

- :point_right: Bạn chạy thử lệnh đó thì hệ thống không báo là `command not found`. Điều này là bình thường vì hệ thống không biết tìm kiếm file nhị phân thực thi cho lệnh đó ở đâu.

- :point_right: Hay nói cách khác, đường dẫn đã không được liệt kê trong biến $PATH.

:bulb: Giải quyết trường hợp trên, đơn giản là điều chỉnh lại biến $PATH và thêm đường dẫn của bạn vào biến này.
