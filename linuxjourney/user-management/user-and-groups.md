# 1. Users and Groups

Trong bất kỳ các hệ điều hành truyền thống nào, đều có hệ thống người dùng và nhóm :star2:. Chúng chỉ tồn tại để cấp quyền truy cập hoặc sử dụng một tài nguyên nào đó.

:bulb: Mỗi người dùng sẽ có một thư mục /home của riêng họ, thường là `/home/username`, nhưng điều này có thể thay đổi tùy vào bản phân phối.

:bulb: HĐH sử dụng user id (UID) để quản lý người dùng, username được xem như là một cách thân thiện hơn để định danh một người dùng, nhưng hđh sẽ định danh một người dùng bằng UID.

:bulb: Hệ thống cũng sử dụng nhóm người dùng để quản lý quyền cho một người dùng, một nhóm sẽ được định danh bằng group id (GID).

:bulb: Trong Linux, bạn sẽ có một số người dùng đặc biệt bên cạnh các người dùng bình thường sử dụng hệ thống. Đôi khi, các người dùng này là các daemon của hệ thống liên tục chạy các tiến trình để duy trì hoạt động của hệ thống.

:boom: Một trong những người dùng quan trọng nhất là người dùng root. Root là người dùng có quyền lực tối cao nhất trong Linux, thậm chí có thể xóa các file hoặc thư mục quan trọng. Cho nên thông thường, bạn không nên sử dụng trực tiếp sử dụng người dùng root.
- :point_right: May mắn là, nếu có đủ quyền, một người dùng bình thường cũng có thể chạy các lệnh dưới quyền root, gọi là lệnh sudo.

Hãy thử dùng một người dùng bình thường và đọc một file trong thư mục được bảo vệ như `/etc/shadow`:

```sh
$ cat /etc/shadow
```

Sau khi chạy lệnh trên với người dùng bình thường, bạn sẽ nhận thấy lỗi truy cập vì không đủ quyền, có thể kiểm tra quyền truy cập thư mục này như sau:

```sh
$ ls -la /etc/shadow
-rw-r----- 1 root shadow 1134 Dec 1 11:45 /etc/shadow
```

:bulb: Chúng ta sẽ tìm hiểu về quyền truy cập sau, nhưng những gì hiển thị ra ở đây đại loại sẽ cho chúng ta biết rằng file này thuộc về người dùng root và chỉ là root hoặc thuộc nhóm người dùng shadow mới có quyền đọc file này.

Bạn có thể "vượt quyền" bằng lệnh sudo:

```sh
$ sudo cat /etc/shadow
```