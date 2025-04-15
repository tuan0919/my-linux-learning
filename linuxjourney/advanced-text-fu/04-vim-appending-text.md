# 4. Vim appending text

Bạn có thể nhận ra rằng trong màn hình Vim editor, bạn không thể gõ bất kì ký tự nào. Đó là do bạn đang ở command mode :boom: 

Điều này có thể khiến cho bạn bị bối rối khi muốn mở một file và sửa nội dung của nó.

Để có thể thay đổi nội dung thì bạn phải chuyển sang insert mode bằng các phím tắt sau:

- i - chèn văn bản vào trước vị trí con trỏ.
- O - chèn văn bản vào dòng trước đó.
- o - chèn văn bản vào dòng tiếp theo.
- a - thêm văn bản vào sau vị trí con trỏ.
- A - thêm văn bản vào cuối dòng.

Lưu ý rằng khi bạn nhập bất kỳ phím nào trong số này, bạn sẽ thấy vim đã vào insert mode ở cuối shell. Để thoát insert mode và quay lại command mode, chỉ cần nhấn phím Esc.
