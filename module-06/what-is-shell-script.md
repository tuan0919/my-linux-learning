[Link bài viết gốc](https://viblo.asia/p/gioi-thieu-ve-linux-shell-va-shell-script-aWj53LweK6m)

### Khái niệm
- Thuờng **shell** sẽ tương tác, có nghĩa là nó sẽ chấp nhận lệnh là đầu vào từ người dùng và thực thi chúng. Tuy nhiên, đôi khi chúng ta muốn thực thi một loạt các lệnh, để làm như thế chúng ta sẽ phải gõ tất cả các lệnh vào terminal. Đ8iều này sẽ làm cho lệnh của chúng ta dài và gây khó hiểu.
- Vì **shell** cũng có thể nhận các lệnh làm đầu vào từ file, chúng ta có thể viết các lệnh trong một file và có thể thực thi chúng trong shell, tránh các công việc lặp đi lặp lại. Các file này được gọi là **Shell Script** hoặc **Shell Program**. Các Shell Script tương tự như batch file trong MS-DOS. Mỗi shell script được lưu với phần mở rộng tệp .sh
- Shell Script bao gồm các thành phần sau:
- Shell Keywords - if, else, break etc.
- Shell commands - cd, ls, echo, pwd, touch etc.
- Functions
- Control flow - if..then..else, case và shell loops etc.
### Tại sao cần shell script?
- Có nhiều lý do để viết shell script:
- Tránh các công việc lặp đi lặp lại và tự động hóa.
- System admins sử dụng shell script để sao lưu thường xuyên.
- Giám sát hệ thống
- Thêm chức năng mới vào một shell có sẵn
### Ưu điểm của shell script
- Lệnh và cú pháp hoàn toàn giống với lệnh được được nhập trực tiếp trong dòng lệnh. Vì vậy lập trình viên không cần phải chuyển sang cú pháp hoàn toàn khác.
- Viết Shell script sẽ nhanh hơn nhiều
- Quick start
- Interactive debugging etc.
### Nhược điểm của shell script
- Dễ xảy ra lỗi tốn kém, một lỗi duy nhất có thể thay đổi lệnh hoặc có thể gây hại.
- Tốc độ thực hiện chậm
- Không phù hợp với các task lớn và phức tạp
- Cung cấp ít cấu trúc dữ liệu không giống các ngôn ngữ khác.
