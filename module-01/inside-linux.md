## Kernel
- Là lõi của hệ thống UNIX. Được load khi hệ thống khởi chạy (boot), là một chương trình điều khiển cư trú trong bộ nhớ (memory-resident control program), nghĩa là một loại phần mềm hệ thống được nạp vào bộ nhớ chính của máy tính và lưu trú tại đó để kiểm soát và quản lý tài nguyên của hệ thống máy tính, chẳng hạn như bộ nhớ, thiết bị ngoại vi và các tiến trình (processes).
- Quản lý toàn bộ tài nguyên của hệ thống, trình bày chúng cho bạn và mọi người dùng khác như một hệ thống nhất quán. Cung cấp dịch vụ cho các ứng dụng người dùng như quản lý thiết bị, lập lịch tiến trình, v.v.
- Một số chức năng được thực hiện bởi Kernel như:
  - Quản lí bộ nhớ của máy và cấp phát chúng cho mỗi tiến trình.
  - Lập lịch các thao tác được thực hiện bởi CPU và nhờ thế các thao tác được thực hiện một cách hiệu quả nhất.
  - Thực hiện việc chuyển dữ liệu từ một phần của máy tính sang phần khác.
  - Diễn giải và thực thi các lệnh từ shell.
  - Thực thi quyền truy cập tệp tin.

## Shell
- Mỗi khi chúng ta login vào hệ thống Unix, chúng ta được đặt vào một chương trình shell. Prompt của shell này thuờng được hiển thị tại vị trí con trỏ trên màn hình của chúng ta. Để hoàn thành công việc của mình, chúng ta nhập lệnh vào promt này.
- Shell là một trình diễn giải lệnh; nó nhận từng lệnh và chuyển nó đến kernel của hệ điều hành để thực thi. Sau đó, nó hiển thị kết quả của thao tác này trên màn hình.
- Trên bất kỳ hệ thống UNIX nào, thường có nhiều loại shell khác nhau, mỗi loại có những ưu điểm và nhược điểm riêng.
- Các người dùng khác nhau có thể sử dụng các shell khác nhau. Ban đầu, quản trị viên hệ thống của bạn sẽ cung cấp một shell mặc định, nhưng bạn có thể thay đổi hoặc ghi đè lên nó. Các shell phổ biến nhất thường có trên hệ thống bao gồm:
  - Bourne shell (sh)
  - C shell (csh)
  - Korn shell (ksh)
  - TC shell (tcsh)
  - Bourne Again shell (bash)
- Mỗi shell cũng bao gồm ngôn ngữ lập trình riêng của nó. Các tệp lệnh, được gọi là "shell scripts," được sử dụng để thực hiện một chuỗi các tác vụ.

## Utilities
- UNIX cung cấp hàng trăm chương trình tiện ích (utilities programs), thường được gọi là các lệnh (commands).
- Các lệnh UNIX thực hiện các chức năng phổ quát, chẳng hạn như:
  - editing
  - file maintenance
  - printing
  - sorting
  - programming support
  - online info etc.
- Tính module: các chương trình đơn lẻ có thể nhóm lại để thực hiện các tác vụ phức tạp.