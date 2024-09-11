### Giới thiệu
Trong hệ điều hành Linux, *job* nghĩa là một process đang chạy background hoặc foreground. *Job control* nghĩa là khả năng thao tác các process này, bao gồm đình chỉ, tiếp tục và terminate chúng. Điều này có thể có ích khi quản lí nhiều task hoặc cần debug một vấn đề gì đó đang xảy ra với process.

*Job control* được thực hiện bởi shell, là giao diện command line cho phép người dùng tương tác với hệ điều hành. Shell nổi tiếng nhất trong Linux là **BASH**, nhưng bên cạnh đó cũng tồn tại một số shell khác nhất như **ZSH** hoặc **KSH**.

### Hiểu về process và jobs trong Linux
Trong Linux, mọi chương trình đang chạy đều được xem là một process. một process có thể là một chương trình đơn lẻ hoặc là một phần của một chương trình lớn hơn.

Mỗi process được gán cho một mã định danh độc nhất được gọi là **PID**. Mã này có thể dùng để đại diện cho process và thực hiện thao tác trên nó, chẳng hạn như đình chỉ hoặc terminate.

Một job là một process *đang chạy background* hoặc *đang chạy foreground*. Foreground là các cửa sổ đang hoạt động bên trong terminal, trong khi đó background là bất kì process nào đang chạy mà không chiếm quyền điều khiển của terminal.

Mặc định thì, khi chúng ta chạy một lệnh trong terminal, thì nó chạy ở foreground. Chúng ta có thể process đang chạy ở foreground vì nó hiển thị output và chúng ta không thể tương tác với terminal cho đến khi lệnh đó hoàn thành hẳn.

Để chạy một process ở background, chúng ta có thể sử dụng kí hiệu *&* ở cuối câu lệnh.

```sh
$ sleep 30 &
[1] 12345
```

Trong ví dụ trên, lệnh **sleep** khiến cho process ngủ 30s. Kí hiệu & khiến cho process chạy background và output **[1] 12345** chỉ ra rằng job number của nó là 1 với PID là 12345.

### Quản lí jobs với lệnh _fg_ và _bg_
Lệnh **fg** (foreground) và **bg** (background) cho phép chúng ta di chuyển job sang foreground hoặc background.

```sh
$ fg %1
sleep 30
```

Mang job của lệnh **sleep** phía trên, có job number là 1 lên foreground và hiển thị output của nó.

Đễ gửi một foreground job xuống background, chúng ta có thể sử dụng lệnh **bg** theo sau là job number hoặc PID.

```sh
$ sleep 30
[1] 12345
^Z
[1]+ Stopped      sleep 30
$ bg %1
[1]+ sleep 30 &
```

Lệnh **sleep** đang chạy ở foreground thì bị đình chỉ bởi phím tắt **^Z**. Sau đó lệnh **bg** được dùng để tiếp tục job này ở dưới background.

### Đình chỉ hoặc Tiếp tục job trong Linux
Lệnh **suspend** cho phép chúng ta dừng tạm thời một job, trong khi đó lệnh **kill** cho phép chúng ta terminated job đó.

Để đình chỉ một job, chúng ta sử dụng **suspend** theo sau là job number hoặc PID.

```sh
$ sleep 30 &
[1] 12345
$ suspend %1
[1]+ Suspended
```

Ví dụ trên đình chỉ lệnh **sleep**, có job number là 1. Job này sau đó có thể tiếp tục với lệnh **fg**.

Để terminate job này, chúng ta có thể sử dụng lệnh **kill** theo sau đó là job number hoặc PID

```sh
$ sleep 30 &
[1] 12345
$ kill %1
```