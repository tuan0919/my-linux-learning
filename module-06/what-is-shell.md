[Link bài viết gốc](https://gnu.org/software/bash/manual/html_node/What-is-a-shell_003f.html)

### Khái niệm
Về cơ bản, shell chỉ đơn giản là một bộ xử lí macro (macro processor) dùng để thực thi các lệnh. Định nghĩa *macro processor* nghĩa là một chức năng mà tại đó các văn bản và kí hiệu được mở rộng ra để tạo thành các biểu thức lớn hơn.

Unix shell vừa là trình thông dịch lệnh, vừa là ngôn ngữ lập trình. Với việc là trình thông dịch lệnh, shell cung cấp một giao diện người dùng với các tiện ích GNU phong phú. Với việc là một ngôn ngữ lập trình, các tiện ích của shell có thể được kết hợp với nhau. Các tập tin chứa các lệnh có thể được tạo ra, và bản thân tập tin đó trở thành một lệnh. Những lệnh mới này có trạng thái giống với các lệnh hệ thống trong các thư mục `/bin`, cho phép người dùng hoặc nhóm người dùng có thể thiết lập các môi trường tùy chỉnh để tự động hóa các common task.

Shell có thể được sử dụng dưới dạng tương tác hoặc không tương tác. Trong chế độ tương tác, chúng nhận một input được nhập vào từ bàn phím. Khi thực thi ở chế độ không tương tác, shell thực thi lệnh đọc được từ một file.

Một shell cho phép thực thi các lệnh GNU, theo hướng đồng bộ hoặc bất đồng bộ. Shell chờ đợi các lệnh đồng bộ được hoàn thành trước khi nhận thêm input; các lệnh bất đồng bộ thì tiếp tục hoạt động một cách song song với shell trong khi nó đọc và thực thi các lệnh khác. Cấu trúc *chuyển hướng* cho phép kiểm soát chi tiết input và output của các lệnh. Hơn nữa, shell cho phép kiểm soát nội dung của môi trường dòng lệnh.

Shell chấp nhận các lệnh có thể đọc được từ người dùng và chuyển đổi chúng thành thứ mà kernel có thể hiểu được.

![img](/images/module-06/f1543025-339d-43f9-948a-ebb559f16cb2.webp)

**Shell** được chia làm hai loại: *Command Line Shell* và *Graphical shell*.

### Command Line Shell
**Shell** có thể được truy cập bởi người dùng bằng cách sử dụng **command line interface**. Một chương trình đặc biệt có tên **Terminal** trong Linux được cung cấp để nhập vào các lệnh có thể đọc được của người dùng như "cat", "ls", và sau đó nó được thực thi. Kết quả sau đó sẽ được hiển thị lên **Terminal**

### Graphical Shell
- **Graphical Shell** cung cấp phương tiện để thao tác với các chương trình dựa trên graphical user interface (GUI), bằng cách cho phép các hoạt động như **open**, **close**, **move** và **resize window**, cũng như chuyển trọng tâm giữa các cửa sổ.
- Window OS hoặc Ubuntu OS có thể được coi là ví dụ điển hình cung cấp GUI cho người dùng để tương tác với chương trình. Người dùng không cần nhập lệnh cho mọi hành động.
- Một số **shell** có sẵn trong các hệ thống Linux:
- BASH (Bourne Again Shell) - Được sử dụng rộng rãi nhất trong các hệ thống Linux. Nó được sử dụng làm vỏ đăng nhập mặc định trong Linux / MacOS. Nó cũng có thể cài đặt trên Window OS.
- CSH (C Shell) - Cú pháp và cách sử dụng của **C Shell** rất giống với ngôn ngữ lập trình C.
- KSH (Korn Shell) - Korn Shell cũng là cơ sở cho các thông số kỹ thuật tiêu chuẩn của POSIX Shell, vv...
- Mỗi shell thực hiện cùng một công việc nhưng hiểu các lệnh khác nhau và cung cấp các hàm dựng sẵn khác nhau.
