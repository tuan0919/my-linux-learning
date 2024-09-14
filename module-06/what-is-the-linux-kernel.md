[Link bài viết gốc](https://www.redhat.com/en/topics/linux/what-is-the-linux-kernel)

### Tổng quan
Linux Kernel là thành phân chính của một hệ điều hành Linux, và là giao diện (interface) chính nằm giữa phần cứng máy tính và process, nó chịu trách nhiệm giao tiếp với 2 bên và quản lí tài nguyên hệ thống một cách hiệu quả nhất có thể.

Sở dĩ được gọi là *Kernel* (hạt nhân) vì - giống như là hạt nằm ở trong một cái vỏ cứng - nó tồn tại trong OS và điều khiển mọi chức năng trọng yếu của phần cứng, kể cả là của điện thoại, laptop, server hay bất kì loại máy tính nào khác.

### Kernel làm gì
Một kernel có 4 nhiệm vụ:

1. **Memory management**: Theo dõi xem bao nhiêu bộ nhớ đã được sử dụng vào việc gì, và ở đâu.
2. **Process management**: Xác định xem process nào sẽ được sử dụng dụng CPU khi nào, bao lâu.
3. **Device drivers**: Đóng vai trò trung gian / thông dịch viên giữa phần cứng và các process.
4. **System calls and security**: Tiếp nhận các yêu cầu dịch vụ từ process.

Kernel, nếu được implement đúng cách, sẽ vô hình đối với người dùng, chỉ hoạt động trong thế giới của riêng nó gọi là *không gian kernel*, là nơi mà nó sẽ cấp phát bộ nhớ và theo dõi cách tất cả mọi thứ được lưu trữ. Tất cả những gì mà người dùng sẽ nhìn thấy - như trình duyệt web và các tập tin - được xem là *không gian người dùng*. Những application này sẽ tương tác với kernel thông qua một system call interface (SCI).

*Nghĩ như thế này*: Kernel là một trợ lí cá nhân rất bận rộn cho một người điều hành quyền lực (phần cứng). Và nhiệm vụ của trợ lí cá nhân là chuyển tiếp các tin nhắn và yêu cầu (từ process) từ các nhân viên và những người bên ngoài (người dùng) đến người điều hành, để biết rằng cái gì được lưu ở đâu (bộ nhớ), và xác định xem ai có quyền liên lạc với người điều hành vào lúc nào và trong bao lâu.

### Kernel làm gì bên trong OS
Để đem kernel vào ngữ cảnh này, chúng ta có thể xem một OS Linux có 3 layer chính:

- **Phần cứng**: Máy chủ vật lí - nằm cuối cùng hoặc là nền của hệ thống, tạo nên bởi bộ nhớ (RAM) và các bộ xử lí hay đơn vị xử lí trung tâm (CPU), cũng như là các thiết bị có input/output như *thiết bị lưu trữ*, *mạng* và *đồ họa*. CPU sẽ thực hiện việc tính toán và đọc từ/viết vào bộ nhớ.
- **Linux Kernel**: Hạt nhân của OS (Nằm ở giữa). Nó là phần mềm nằm trong bộ nhớ mà sẽ cho biết CPU cần phải làm gì.
- **User process**: Là các chương trình đang chạy sẽ được kernel quản lí. User process là những gì sẽ tạo nên *không gian người dùng*. Kernel cũng cho phép các process này và server giao tiếp với nhau (còn được gọi là inter-process communication hay IPC).

Code được thực thi bởi hệ thống khi chạy trên CPU sẽ ở một trong hai chế độ: *Kernel mode* hoặc *user mode*. Code chạy ở *kernel mode* có quyền truy cập không bị hạn chế đối với các thiết bị phần cứng, trong khi đó code chạy ở *user mode* sẽ bị quyền truy cập hạn chế hơn vào CPU và bộ nhớ thông qua SCI (System call interface). Sự phân biệt tương tự cũng áp dụng cho bộ nhớ (giữa không gian kernel và không gian người dùng). 

Điều này cũng có nghĩa là nếu một process failed ở user mode, thiệt hại sẽ được hạn chế và có thể được phục hồi thông qua kernel. Tuy nhiên, bởi quyền truy cập của nó vào các bộ xử lí và bộ nhớ, kernel process crash có thể kéo theo sập toàn bộ hệ thống. Vì có sẵn các biện pháp bảo vệ và các quyền cần thiết để vượt qua ranh giới nên sự cố trong quy trình của người dùng thường không thể gây ra quá nhiều vấn đề.
