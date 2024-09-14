### Variables
Trong Linux có hai loại biến:
- Biến hệ thống: Được tạo và duy trì bởi chính Linux. Thường được viết theo định dạng UPPERCASE.
- Biến do người dùng định nghĩa: Được tạo và duy trì bởi người dùng. Thường được viết theo định dạng lowercase.

Cách định nghĩa biến: `variable_name=variable_value`
- `variable_name`: Phải bắt đầu bằng ký tự chữ và số hoặc dấu gạch dưới. Ví dụ: HOME, user_name...
- Không đặt dấu cách ở hai bên của dấu bằng khi gán giá trị cho biến. Ví dụ `$no= 1`, `$no= 1`, `$$no = 1`.
- Các biến có phân biệt chữ hoa, chữ thường, giống như filename trong Linux.
- Có thể định nghĩa biến NULL như sau: `$no=`, `$no=""`
Để xem giá trị của biến ta sử dụng lệnh: `echo $VARIABLE_NAME`

Biến chỉ đọc: giá trị của nó không thể thay đổi - Cú pháp `readonly variable_name`
```sh
NAME="Zara Ali"
readonly NAME
NAME="Qadiri"
```
Hủy một biến - Cú pháp `unset variable_name`
```sh
NAME="Zara Ali"
unset NAME
echo $NAME
```
### Special variables (*)
Chúng ta không thể sử dụng các ký tự đặc biệt như `! @ $ ...` để đặt tên cho biến. Điều này là do các ký tự đó được sử dụng trong các biến đặc biệt của Linux. Các biến này được dành riêng cho các chức năng cụ thể:
|No|Variable & Description|
|--|--------|
|1 |`$0` - Tên tệp của lệnh/tập lệnh hiện tại |
|2 |`$n` - Các biến này tương ứng với các đối số truyền vào, n là số nguyên dương. Ví dụ: `./test.sh a b` thì đối số `$1`, `$2` lần lượt là a và b |
|3 |`$#` - Số lượng đối số truyền vào. Vd: `./test.sh a b` sẽ có 2 đối số |
|4 |`$?` - Trạng thái thoát ra của lệnh trước được chạy (thường là 0 đại diện cho lệnh trước chạy thành công, khác 0 là failed) Max range [0 - 255] |
|5 |`$$` - Số tiến trình của shell hiện tại. Đối với Shell Script thì đây là số processID mà nó đang chạy |
|6 |`$!` - Process number của lệnh background cuối cùng |
|7 |`$*` - Chứa tất cả các đối số truyền vào. Nếu có 3 đối số truyền vào thì giá trị sẽ là `$1` `$2` `$3` khi sử dụng |
|8 |`$@` - Chứa tất cả các đối số truyền vào nhưng phân tách thành các đối số riêng lẻ không như `$*`|
### Basic Operators
Về cơ bản Shell Linux sử dụng các toán tử cơ bản như các ngôn ngữ lập trình khác như C/C++, Java, ...
#### 1. Toán tử số học
- Ban đầu Shell không có bất kỳ cơ chế nào để thực hiện các phép toán số học, nhưng nó đã sử dụng các chương trình bên ngoài như **awk** hoặc **expr** để thực thi.
- Ví dụ sau cho thấy cú pháp cộng 2 số:
```sh
#!/bin/sh

sum=`expr 3 + 2`
echo "Total value: $sum"
```
- Chạy lệnh trên thì kết quả là 5
- Những điều cần lưu ý trong phép toán trên là:
- Giữa các toán tử và các biểu thức phải có dấu **khoảng trắng**. Ví dụ **2+2** là không đúng, nên được viết là **2 + 2**
- Biểu thức hoàn chỉnh phải được đặt trong dấu \`<biểu thức>`, được gọi là **backtick**.
- Các toán tử số học được shell hỗ trợ, Giả sử biến a=10, biến b=20

|Toán tử|Mô tả|Ví dụ|
|-------|-----|-----|
|+|Phép cộng|`expr $a + $b` = 30|
|-|Phép trừ|`expr $a - $b` = -10|
|*|Phép nhân|`expr $a * $b` = 200|
|/|Phép chia|`expr $b / $a` = 2|
|%|Phép chia lấy dư|`expr $b % $a` = 0|
|=|Phép gán|`a = $b` Gán giá trị của b cho a|
|==|Phép so sánh bằng|`[ $a == $b ]` = false|
|!=|Phép so sánh khác|`[ $a != $b ]` = true|
- Có một điều quan trọng cần lưu ý là các *biểu thức điều kiện* phải nằm trong dấu `[]` có khoảng trắng xung quanh
- Tất cả các phép toán số học được thực hiện bằng cách sử dụng long interger.

#### 2. Toán tử quan hệ
- Shell hỗ trợ các toán tử quan hệ sau đây **dành riêng cho các giá trị số**. Các toán tử này **không hoạt động cho các giá trị chuỗi** trừ khi giá trị của chúng là số.
- Giả sử $a=10 và $b=20:

|Toán tử|Mô tả|Ví dụ|
|-------|-----|-----|
|`-eq`(Equal)|Kiểm tra giá trị của 2 toán hạng có bằng nhau không|`[ $a -eq $b]` = false|
|`-ne`(Not Equal)|Kiểm tra giá trị của 2 toán hạng có khác nhau không|`[ $a -ne $b ]` = true|
|`-gt`(Greater than)|Kiểm tra giá trị của toán hạng trái có lớn hơn giá trị của toán hạng phải không|`[ $a -gt $b ]` = false|
|`-lt`(Less than)|Kiểm tra giá trị của toán hạng trái có nhỏ hơn giá trị của toán hạng phải không|`[ $a -lt $b ]` = true|
|`-ge`(Greater or Equal)|Kiểm tra giá trị của toán hạng trái có lớn hơn hoặc bằng giá trị toán hạng phải không|`[ $a -ge $b ] = false`|
|`-le`(Less or Equal)|Kiểm tra giá trị của toán hạng trái có nhỏ hơn hoặc bằng giá trị toán hạng phải không|`[ $a -le $b ] = true`|

#### 3. Toán tử boolean

Các toán tử Boolean sau đây được Shell hỗ trợ. Giả sử $a=10, $b=20.

|Toán tử|Mô tả|Ví dụ|
|-------|-----|-----|
|!|Phủ định logic|`[ ! false ]` = true|
|-o|Phép OR|`[ $a -lt -o $b -gt 100 ]` = true|
|-a|Phép AND|`[ $a -lt 20 -a -gt 100 ]` = false|

#### 4. Toán tử String

Giả sử $a="abc", $b="efg":

|Toán tử|Mô tả|Ví dụ|
|-------|-----|-----|
|=|Kiểm tra xem giá trị của 2 toán hạng có bằng nhau không|`[ $a = $b ]` = false|
|!=|Kiểm tra xem giá trị của 2 toán hạng có khác nhau không|`[ $a != $b ]` = true|
|-z|Kiểm tra độ dài toán hạng có bằng 0 không|`[ -z $a ]` = false|
|-n|Kiểm tra độ dài toán hạng có khác 0 không|`[ -n $a ]` = true|
|str|Kiểm tra chuỗi str có khác empty hay không|`[ $a ]` = true|

#### 5. Toán tử kiểm tra file

Giả sử biến $file trỏ đến một file có tên là "test", kích thước của file đó là 100 byte và có quyền **read, write, execute**.

|Toán tử|Mô tả|Ví dụ|
|-------|-----|-----|
|-b file|Kiểm tra file có block special file|`[ -b $file ]` = false|
|-c file|Kiểm tra file có là character special file|`[ -c $file ]` = false|
|-d file|Kiểm tra file có phải là thư mục|`[ -d $file ]` = false|
|-f file|Kiểm tra file có là file thông thường, không phải thư mục hoặc special file|`[ -f $file ]` = true|
|-g file|Kiểm tra file có cài đặt nhóm bit ID (SGID) không|`[ -g $file ]` = false|
|-k file|Kiểm tra file có cài đặt sticky bit không|`[ -k $file ]` = false|
|-p file|Kiểm tra file là một named pipe không|`[ -p $file ]` = false|
|-t file|Kiểm tra mô tả file có mở và liên kết với terminal|`[ -t $file ]` = false|
|-u file|Kiểm tra file có cài đặt Set User ID (SUID) không|`[ -u $file ]` = false|
|-r file|Kiểm tra file có thể đọc không|`[ -r $file ]` = true|
|-w file|Kiểm tra file có thể ghi không|`[ -w $file ]` = true|
|-x file|Kiểm tra file có thể execute không|`[ -x $file ]` = true|
|-s file|Kiểm tra kích thước file có lớn hơn 0 không|`[ -s $file ]` = true|
|-e file|Kiểm tra file có tồn tại không. Đúng ngay cả khi file là thư mục|`[ -e $file ]` = true|
