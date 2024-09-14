### 1. Câu lệnh điều kiện
Có 5 câu lệnh điều kiện trong lập trình Shell:
- if statement
- if-else statement
- if..elif..else..fi statement
- if..then..else..if..then..fi..fi..(Nested if)
- switch statement 
#### Syntax

##### If statement
```sh
if [ expression ]
then
statement
fi
```

##### if-else statement
```sh
if [ expression ]
then
statement1
else
statement2
fi
```

##### if..elif..else..fi statement
```sh
if [ expression1 ]
then
statement1
statement2
.
.
elif [ expression2 ]
then
statement3
statement4
.
.
else
statement5
fi
```

##### if..then..else..if..then..fi..fi..(Nested if)
```sh
if [ expression1 ]
then
statement1
statement2
.
else
if [ expression2 ]
then
    statement3
    .
fi
fi
```

##### switch statement
```sh
case  in
Pattern 1) Statement 1;;
Pattern n) Statement n;;
esac
```

### 2. Mảng trong Shell
#### Định nghĩa mảng
- Define: `array_name[index]=value`
- array_name: Tên của mảng.
- index: là chỉ mục.
- value: giá trị tại chỉ mục đó.
- Ví dụ:
```sh
NAME[0]="Zara"
NAME[1]="Qadir"
NAME[2]="Mahnaz"
NAME[3]="Ayan"
NAME[4]="Daisy"
```
- Nếu chúng ta sử dụng **KornShell** cú pháp khởi tạo mảng: `set -A array_name value1 value2 ... valueN`
- Nếu chúng ta đang sử dụng **BashShell** cú pháp khởi tạo mảng: `array_name=(value1 ... valueN)`
#### Truy cập giá trị mảng
- Cú pháp để truy cập giá trị mảng : `${array_name[index]}`
- Xem xét ví dụ sau, tạo file test.sh:
```sh
#!/bin/bash

NAME[0]="Zara"
NAME[1]="Qadir"
NAME[2]="Mahnaz"
NAME[3]="Ayan"
NAME[4]="Daisy"
echo "First Index: ${NAME[0]}"
echo "Second Index: ${NAME[1]}"
```
- Kết quả ví dụ trên:
```sh
$./test.sh
First Index: Zara
Second Index: Qadir
```
- Chúng ta cũng có thể truy cập tất cả các item trong mảng với cú pháp sau:
```sh
${array_name[*]}
${array_name[@]}
```
- Xem ví dụ sau:
```sh
#!/bin/bash

NAME[0]="Zara"
NAME[1]="Qadir"
NAME[2]="Mahnaz"
NAME[3]="Ayan"
NAME[4]="Daisy"
echo "First Method: ${NAME[*]}"
echo "Second Method: ${NAME[@]}"
```
- Kết quả:
```sh
$./test.sh
First Method: Zara Qadir Mahnaz Ayan Daisy
Second Method: Zara Qadir Mahnaz Ayan Daisy
```
### 3. Vòng lặp
- Shell hỗ trợ các loại vòng lặp sau:
- while loop
- for loop
- until loop
- select loop
- Có thể thay đổi trạng thái của vòng lặp bằng lệnh `break`, `continue`.
- Chúng ta cũng có thể sử dụng các vòng lặp lồng nhau

#### While loop
- Syntax:
```sh
while command
do
statement(s)
done
```
- Ví dụ: In ra các số nguyên nhỏ hơn 10.
```sh
#!/bin/bash

a=0
while [ $a -lt 10 ]
do
echo $a
a=`expr $a + 1`
done
```
- Kết quả:
```sh
0
1
2
3
4
5
6
7
8
9
```
#### For loop
- Syntax:
```sh
for var in word1 word2 ... wordN
do
Statement(s) to be executed for every word.
done
```
- Ví dụ:
```sh
#!/bin/bash

for var in 0 1 2 3 4 5 6 7 8 9
do
echo $var
done
```
- Kết quả:
```sh
0
1
2
3
4
5
6
7
8
9
```

#### Until loop
- Vòng lặp until cho phép thực hiện một lệnh cho đến khi một điều kiện trở thành đúng. Có nghĩa là nếu điều kiện false thì tập lệnh sẽ được thực thi, còn nếu điều kiện là true thì sẽ không có câu lệnh nào được thực thi. Có nghĩa là **until loop** giống với **do..while** trong các ngôn ngữ lập trình khác.
- **Until loop** luôn thực thi ít nhất 1 lần.
- Syntax:
```sh
until command
do
Statement(s) to be executed until command is true
done
```
- Ví dụ: Hiển thị các số từ 0 đến 9
```sh
#!/bin/bash
a=0
until [ ! $a -lt 10 ]
do
echo $a
a=`expr $a + 1`
done
```

#### Select loop
- Vòng lặp Select giúp tạo một menu được đánh số theo thứ tự, giúp người dùng có thể tự chọn.
- Syntax:
```sh
select var in word1 word2 ... wordN
do
Statement(s) to be executed for every word.
done
```
- Ví dụ:
```sh
#!/bin/bash

PS3='Please enter your choice: '
select DRINK in tea cofee water juice appe all none
do
case $DRINK in
    tea|cofee|water|all) 
        echo "Go to canteen"
        ;;
    juice|appe)
        echo "Available at home"
    ;;
    none) 
        break 
    ;;
    *) echo "ERROR: Invalid selection" 
    ;;
esac
done
```
- Kết quả:
```sh
1) tea
2) cofee
3) water
4) juice
5) apple
6) all
7) none
Please enter your choice: 1
Go to canteen
Please enter your choice:
```

### 4. Functions
#### Tạo hàm
```sh
function_name () {
<list of commands>
}
```
- Ví dụ:
```sh
#!/bin/bash
# Define your function here
hello () {
echo "Hello World"
}
# Invoke your function
hello
```
#### Truyền tham số vào hàm
- Chúng ta có thể định nghĩa một hàm sẽ chấp nhận các tham số trong khi gọi hàm, các tham số sẽ được biểu thị bởi $1, $2...
```sh
#!/bin/bash
# Define your function here
hello () {
echo "Hello World $1 $2"
}
# Invoke your function
hello Zara Ali
```
#### Trả về giá trị trong hàm
- Để trả về giá trị từ một function ta sử dụng lệnh **return**
- Ví dụ: Trả về giá trị 10
```sh
Live Demo
#!/bin/bash
# Define your function here
hello () {
echo "Hello World $1 $2"
return 10
}
# Invoke your function
hello Zara Ali
# Capture value returnd by last command
ret=$?
echo "Return value is $ret"
```
### 5. Shell Substitution
- Shell thực hiện thay thế khi gặp các ký tự đặc biệt. Xem ví dụ:
```sh
#!/bin/bash
a=10
echo -e "Value of a is $a \n"
```
- Option **-e** cho phép thực thi backlash escapes `Value of a is 10`. Và đây là kết quả khi không có **-e**: `Value of a is 10\n`
- Một số escape được sử dụng trong lệnh echo:
- **\\**: backslash
- **\a**: alert
- **\b**: backspace
- **\c**: suppress trailing newline
- **\f**: form feed
- **\n**: newline
- **\r**: carriage return
- **\t**: horizontal tab
- **\v**: vertical tab
- Có thể sử dụng option **-E** để disable backslash, **-n** để disable newline.
- **Command substitution**: là cơ chế mà shell thực hiện một tập lệnh đã cho và sau đó thay thế đầu ra của nó ở nơi được gọi.
- Syntax: `command`. Sử dụng dấu \```, **không phải** single quote.
- Xem xét ví dụ:
```sh
#!/bin/bash
DATE=`date`
echo "Date is $DATE"
USERS=`who | wc -l`
echo "Logged in user are $USERS"
UP=`date ; uptime`
echo "Uptime is $UP"
```
- Kết quả:
```sh
Date is Thu Jul  2 03:59:57 MST 2009
Logged in user are 1
Uptime is Thu Jul  2 03:59:57 MST 2009
03:59:57 up 20 days, 14:03,  1 user,  load avg: 0.13, 0.07, 0.15
```
- **Variable Substitution**: cho phép thao tác giá trị của variable dựa trên trạng thái của nó.
- `${var}`: Thay thế giá trị của var
- `${var:-word}`: Nếu var là `null` hoặc `unset`, word được thay thế cho var. Giá trị của var không thay đổi.
- `${var:=word}`: Nếu var là `null` hoặc `unset`, var được đặt thành giá trị của word.
- `${var:?message}`: Nếu var là `null` hoặc `unset`, message được in thành lỗi tiêu chuẩn. Điều này kiểm tra các biến được đặt chính xác.
- `${var:+word}`: Nếu var được `set`, word được thay thế cho var. Giá trị của var không thay đổi.
- Ví dụ:
```sh
#!/bin/bash

echo ${var:-"Variable is not set"}
echo "1 - Value of var is ${var}"

echo ${var:="Variable is not set"}
echo "2 - Value of var is ${var}"

unset var
echo ${var:+"This is default value"}
echo "3 - Value of var is $var"

var="Prefix"
echo ${var:+"This is default value"}
echo "4 - Value of var is $var"

echo ${var:?"Print this message"}
echo "5 - Value of var is ${var}"
```
- Kết quả:
```sh
Variable is not set
1 - Value of var is
Variable is not set
2 - Value of var is Variable is not set

3 - Value of var is
This is default value
4 - Value of var is Prefix
Prefix
5 - Value of var is Prefix
```