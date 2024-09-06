# Khái niệm
UNIX và các hệ điều hành giống UNIX (như Linux) bao gồm một Kernel và một số chương trình hệ thống (system program). Ngoài ra, còn có các chương trình ứng dụng (application program) để thực thi công việc. Kernel là phần cốt lõi của hệ điều hành. Thực tế thì Kernel thường bị nhầm lẫn là hệ điều hành nhưng không phải vậy. Hệ điều hành bản thân nó cung cấp nhiều dịch vụ hơn so với Kernel.

Nó theo dõi các tập tin trên đĩa, khởi động chương trình và chạy chúng một cách đồng thời, cấp phát bộ nhớ và các tài nguyên khác nhau cho nhiều process, nhận các packet và gửi chúng thông qua mạng và tương tự như vậy. Kernel bản thân nó thực hiện rất ít việc, nhưng nó cung cấp các công cụ mà các dịch vụ có thể được xây dựng dựa trên. Ngoài ra nó cũng ngăn chặn bất kì ai truy cập trực tiếp vào các phần cứng, ép họ sử dụng các công cụ mà nó cung cấp. Với cách này Kernel sẽ cung cấp được một số bảo vệ cho người dùng. Các công cụ được cung cấp bởi Kernel được sử dụng thông qua system call.

Các system program sử dụng tool được cung cấp bởi Kernel để implement một số service được yêu cầu bởi hệ điều hành. System program, và tất cả các loại program khác, chạy *on top* của một Kernel, hay còn được gọi là *user mode*. Sự khác biệt giữa *system program* và *application program* nằm ở mục đích sử dụng:
- **application program - chương trình ứng dụng**: được thiết kế để thực thi các công việc tiện ích (để giải trí, nếu đó là một trò chơi). Ví dụ: chương trình xử lí văn bản là một chương trình ứng dụng.
- **system program - chương trình hệ thống**: là cần thiết để cho hệ thống hoạt động. Ví dụ: lệnh **mount** là một chương trình hệ thống .

Tuy nhiên sử khác biệt này thường khá mơ hồ và chỉ quan trọng khi chúng ta thật sự chú trọng vào việc phải phân loại chúng.