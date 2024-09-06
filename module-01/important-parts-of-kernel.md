# Khái niệm
Linux Kernel bao gồm các thành phần quan trọng:

- Process Management
- Memory Management
- Hardware device drivers.
- Filesystem drivers.
- Network Management.
- Various other bits and pieces.

Hình sau cho chúng ta thấy một số thành phần quan trọng của Linux Kernel:

![img](/images/img2.gif)

Có lẽ các phần quan trọng nhất của Kernel (không thứ gì có thể hoạt động mà không có chúng) là memory management và process management. Memory Mangement sẽ lo việc cấp phát các không gian bộ nhớ và swap các không gian đến process, đến các phần của kernel và đến các bộ nhớ đệm. Process Management sẽ tạo ra các process, và implement tính đa nhiệm bằng cách chuyển đổi process hoạt động trên processor.

Ở mức độ thấp nhất, kernel (nhân hệ điều hành) chứa một driver thiết bị phần cứng cho mỗi loại phần cứng mà nó hỗ trợ. Vì thế giới đầy rẫy các loại phần cứng khác nhau, số lượng driver thiết bị phần cứng là rất lớn. Thường thì có nhiều phần cứng tương tự nhau nhưng khác nhau về cách điều khiển bằng phần mềm. Sự tương đồng này cho phép có các lớp driver tổng quát hỗ trợ các hoạt động tương tự; mỗi thành viên của lớp đó có cùng giao diện với phần còn lại của kernel nhưng khác nhau ở những gì cần làm để thực hiện các hoạt động đó. Ví dụ, tất cả các driver ổ đĩa đều giống nhau với phần còn lại của kernel, tức là chúng đều có các hoạt động như `khởi tạo ổ đĩa`, `đọc sector N`, và `ghi sector N`.