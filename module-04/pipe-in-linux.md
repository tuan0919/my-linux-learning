## Mở đầu
Trong **Linux**, các thao tác chủ yếu và thường xuyên của người sử dụng là việc gõ các dòng lệnh trên một cửa sổ Terminal. Mỗi câu lệnh của Linux thường sẽ bao gồm đầu vào input và đầu ra output, ngoài ra phần lớn câu lệnh cũng đi kèm theo các thông báo lỗi. Nguyên lí thiết kế của các chương trình trong linux là chỉ làm một nhiệm vụ và làm nhiệm vụ đó tốt nhất có thể. Tuy nhiên các công việc của người sử dụng lại không chỉ đơn giản là sử dụng một câu lệnh duy nhất mà cần nhiều chương trình phối hợp với nhau để cùng thực hiện. Điều này thể hiện ở việc đầu ra của chương trình này lại là đầu vào của chương trình khác. Và như vậy theo cách thông thường chúng ta thường sẽ chạy từng câu lệnh riêng biệt, và lấy đầu ra của câu lệnh này làm đầu vào của câu lệnh kia, việc này mất rất nhiều vì đầu ra của các chương trình thường rất dài và phức tạp. Trong Linux, có một tính năng giúp người dùng sử dụng có thể giảm tải lượng công việc quá mất thời gian công sức này, đó là Piping - tính năng giúp chuyển hướng dòng thực thi của câu lệnh.

## Cơ bản về Piping
Về cơ bản piping là một dạng chuyển hướng được sử dụng trong các dòng hệ điều hành Linux dùng để chuyển đầu ra của chương trình cho chương trinh khác làm đầu vào để xử lí tiếp. Theo ý nghĩa, **piping** là một đường ống, tức là nó sẽ làm cho các câu lệnh trở thành một dòng xử lý nối tiếp nhau và liên tục, kết nối trực tiếp và tạm thời hai hoặc nhiều chương trình đơn giản thành một nhóm các chương trình phức tạp. Chính nhờ vậy mà một số nhiệm vụ có thể hoàn thành với hiệu suất cao mà không một chương trình riêng lẻ nào có thể thực hiện một mình được. Việc kết nối chương trình thông qua **piping** giúp cho các chương trình có thể hoạt động liên tục chứ không phải chờ dữ liệu từ các nơi lưu trữ tạm thời như tệp tin hoặc màn hình hiển thị, cũng không phải chờ cho chương trình trước đó hoàn thành mà có thể hoạt động ngay khi chương trình trước nó bắt đầu tạo dữ liệu đầu ra.

## Luồng dữ liệu
Các chương trình trong Linux được kế tnối với 3 luồng dữ liệu khi chúng được thực thi:
- **stdin** (standard input): là luồng sẽ đưa dữ liệu vào chương trình để xử lí.
- **stdout** (standard output): luồng này dùng để truy xuất dữ liệu ra màn hình hiển thị sau quá trình thực thi hoàn tất mà không gặp lỗi.
- **stderr** (standard error): luồng này có chức năng tương tự như **stdout**, tuy nhiên nó chỉ dùng để in các thông báo lỗi và đồng thời khi đó tín hiệu lỗi cũng được gửi

![img](/images/4e0cf086-add6-4ae9-ae17-911df8a6038a.webp)

Ngoài ra, tùy theo chương trình mà luồng **stdout** có thể là tệp tin hoặc máy in...

Việc liên kết các chương trình sẽ là việc đưa dữ liệu đầu vào chương trình trước đó đến thẳng đầu vào của chương trình sau mà không gặp dữ liệu được in ra màn hình hiển thị hoặc file.

## Các dạng chuyển hướng
### Chuyển hướng tới file
- Là một trong 2 cách chuyển hướng đơn giản nhất, với cách này dữ liệu đầu ra sẽ được lưu vào file thay vì in ra màn hình hiển thị.
- Để chuyển hướng 1 câu lệnh đến file, Linux cung cấp cho người dùntg sử dụng 2 cú pháp `<` (ghi nội dung ra file từ điểm bắt đầu, nếu file đã fcó nội dung thì ghi đè) và `<<` (tương tự `<` nhưng thay vì ghi đè nội dung cũ thì ghi từ điểm kết thúc của nội dung cũ).

> Ghi nội dung ra file, nếu file không tồn tại thì file mới sẽ được tạo

```sh
echo 'Hello World' > newfile.txt
cat newfile.txt
> Hello World
```
### Chuyển hướng từ file
- Là cách chuyển hướng đơn giản còn lại, đi cùng với **Chuyển hướng tới file**, cách này giống với việc đọc dữ liệu từ file và sử dụng đó làm đầu vào cho chương trình.
- Chỉ có một kí hiệu duy nhất cho cách này là `<` (Không có `>`)

> Trong ví dụ này, nội dung của file được dùng làm đầu vào cho câu lệnh `wc`, có thể thấy rõ sự khác biệt của lần thực thi. Lần 1 thì đầu vào là 1 file, lần 2 thì đầu vào chỉ là nội dung của file (output của `wc` không còn tên file nữa)

```sh
wc old_file
> 2 5 32  old_file
wc < old_file
> 2 5 32
```
### Chuyển hướng đến stderr
- Thông thường khi một câu lệnh gặp lỗi, thông tin lỗi sẽ hiển thị luôn trên màn hình cùng với các dữ liệu đầu ra.
- Linux cung cấp kí hiệu `2>` để đưa nội dung thông báo lỗi ra file thay vì màn hình hiển thị.

### Chuyển hướng tối câu lệnh khác
- Sự chuyển hướng đặc biệt nhất, chuyển hướng **stdout** của một câu lệnh thành một **stdin** của câu lệnh tiếp theo
- Sử dụng kí hiệu `|` để chuyển hướng

```sh
printf 'Line1\nLine2\n' | wc -l
> 2
```