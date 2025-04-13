# 1. stdout (Standard out)

Đầu tiên, chúng ta hãy cùng nhau chạy lệnh sau rồi sau đó sẽ phân tích cách mà nó hoạt động:

```sh
$ echo Hello World > peanuts.txt
```

:open_mouth: Chuyện gì đã xảy ra? Hãy thử kiểm tra thư mục hiện tại mà bạn đã chạy lệnh trên, bạn sẽ thấy một file peanuts.txt, bên trong file này sẽ có nội dung là "Hello World". 

Điều này chứng tỏ có khá nhiều thứ đã xảy ra với lệnh trên, hãy cùng tìm hiểu với mình.

Đầu tiên thì, hãy tách phần đầu tiên của lệnh ra:

```sh
$ echo Hello World
```

Chúng ta đều biết rằng lệnh này sẽ in ra một chữ Hello World tại màn hình, nhưng tại sao? 

- :bulb: Các tiến trình sẽ sử dụng một luồng I/O để nhận đầu vào và trả kết quả về tại một đầu ra. 

- :bulb: Đầu vào mặc định được gọi là **stdin** còn đầu ra mặc định được gọi là **stdout**.

- :bulb: Mặc định thì lệnh echo sẽ nhận đầu vào là từ bàn phím và trả đầu ra đến màn hình.

Đấy là lí do mà khi chúng ta gõ echo Hello World, chúng ta nhận được chữ Hello World trên màn hình :smiley:.

Tuy nhiên, thực tế chúng ta đã không để nó trả đầu ra đến màn hình, mà đã "chuyển hướng" đầu ra đến một file.

- :point_right: Việc chuyển hướng này mang lại cho chúng ta tính linh hoạt cao hơn trong các tác vụ thao tác với tệp.

Hãy xem xét phần tiếp theo của lệnh

```sh
>
```

Thằng này là toán tử chuyển hướng cho phép chúng ta chuyển hướng đầu ra mặc định. Nhờ nó mà từ Hello World của chúng ta thay vì gửi đến màn hình thì được gửi đến một file khác. 

:sparkles: Nếu file đó không tồn tại thì toán tử này cũng tạo mới luôn.

:collision: Nếu file đã tồn tại thì nội dung file sẽ bị ghi đè hết!

Và đó là cơ bản về cái cách mà chúng ta đã thực hiện chuyển hướng stdout.

À, trong trường hợp muốn chuyển hướng stdout nhưng không muốn ghi đè nội dung file thì may mắn là Linux cung cấp luôn toán tử `>>` để làm việc này rồi:

```sh
$ echo Hello World >> peanuts.txt
```

Lệnh này vẫn sẽ chuyển hướng nội dung stdout vào file peanuts.txt nhưng sẽ thêm vào cuối file thay vì ghi đè toàn bộ nội dung của file như trước đó.