# Wild Cards trong Linux

Wildcards là các kí tự đặc biệt có thể sử dụng để đại diện cho một lớp các kí tự trong các câu lệnh tìm kiếm.

- `*`: Đại diện cho 0 hoặc nhiều hơn 1 kí tự.
- `?`: Đại diện cho một kí tự bất kì.
- `[]`: Đại diện cho một tập hợp các ký tự đơn lẻ mà bạn muốn khớp.
- `{}`: Đại diện cho một tập hợp các từ hoặc chuỗi (có thể sử dụng để tạo nhiều file)

Ví dụ:
- `rm abc*`: xóa tất cả các tài nguyên bắt đầu với `abc`.
- `touch abc{1..9}-xyz`: tạo 9 file `abc{1 -> 9}-xyz`.