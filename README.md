# my-linux-learning

Đây là repository dùng để ghi chú lại các thông tin quan trọng trong quá trình học và sử dụng hệ điều hành Linux của mình.

## Table of Contents


<details>
<summary>
<b>Module 1 - Understanding Linux Concepts</b>
</summary>

1. **[Unix vs Linux](module-01/unix-vs-linux.md)**

2. **[Hard disk](module-01/hard-disk.md)**

3. **[Disk cache](module-01/disk-cache.md)**

4. **[Inside Linux](module-01/inside-linux.md)**

5. **[Operating System](module-01/operating-system.md)**

6. **[Various Parts of an Operating System](module-01/various-parts-of-os.md)**

7. **[Important parts of Kernel](module-01/important-parts-of-kernel.md)**

8. **[Virtual Memory](module-01/virtual-memory.md)**

</details>

<details>
<summary>
<b>Module 2 - Install VMWare</b>
</summary>

*Chưa có gì phải ghi chú ở đây*
</details>

<details>
<summary>
<b>Module 3 - System Access And File System</b>
</summary>

1. **[Something that need to remember](module-03/important-things-to-remember.md)**

2. **[Linux File System](module-03/linux-file-system.md)**

3. **[File System Structure and its Description](module-03/file-system-structure.md)**

4. **[Navigating File System](module-03/navigating-file-system.md)**

5. **[What is root](module-03/what-is-root.md)**

6. **[Creating files, file types](module-03/creating-files-directories.md)**

7. **[Find files](module-03/find-files.md)**

8. **[WildCards](module-03/wild-cards.md)**

9. **[Soft and hard links in details](module-03/soft-and-hard-links-in-details.md)**

</details>

<details>
<summary>
<b>Module 4 - Linux Fundamentals</b>
</summary>

1. **[Linux Command Syntax](module-04/linux-command-syntax.md)**

2. **[Access Permission (In Details)](module-04/access-permission.md)**

3. **[Access Control List - ACL (In Details)](module-04/access-control-list.md)**

4. **[Pipe In Linux (In Details)](module-04/pipe-in-linux.md)**

5. **[Filtering In Linux](module-04/filtering-in-linux.md)**

</details>

<details>
<summary>
<b>Module 5 - System Adminstration</b>
</summary>

1. **[User & Group Management (In details)](module-05/user-group-management.md)**

2. **[Process and Threads (QNX Neutrino Terms)](module-05/process-and-threads-qnx-neutrino-terms.md)**

3. **[Process in Linux/Unix](module-05/process-in-linux.md)**

4. **[Jobs and Job Control in Linux](module-05/jobs-in-linux.md)**

</details>

<details>
<summary>
<b>Module 6 - Shell Scripting</b>
</summary>

- <details>
  <summary><b>What is the Linux Kernel?</b></summary>

  [Link bài viết gốc](https://www.redhat.com/en/topics/linux/what-is-the-linux-kernel)

  ### Tổng quan
  Linux Kernel là thành phân chính của một hệ điều hành Linux, và là giao diện (interface) chính nằm giữa phần cứng máy tính và process, nó chịu trách nhiệm giao tiếp với 2 bên và quản lí tài nguyên hệ thống một cách hiệu quả nhất có thể.

  Sở dĩ được gọi là *Kernel* (hạt nhân) vì - giống như là hạt nằm ở trong một cái vỏ cứng - nó tồn tại trong OS và điều khiển mọi chức năng trọng yếu của phần cứng, kể cả là của điện thoại, laptop, server hay bất kì loại máy tính nào khác.

  ### Kernel làm gì
  Một kernel có 4 nhiệm vụ:

  1. **Memory management**: Theo dõi xem bao nhiêu bộ nhớ đã được sử dụng vào việc gì, và ở đâu.
  2. **Process management**: Xác định xem process nào sẽ được sử dụng dụng CPU khi nào, bao lâu.
  3. **Device drivers**: Đóng vai trò trung gian / thông dịch viên giữa phần cứng và các process.
  4. **System calls and security**: Tiếp nhận các yêu cầu dịch vụ từ process.
   
  Kernel, nếu được implement đúng cách, sẽ vô hình đối với người dùng, chỉ hoạt động trong thế giới của riêng nó gọi là *không gian kernel*, là nơi mà nó sẽ cấp phát bộ nhớ và theo dõi cách tất cả mọi thứ được lưu trữ. Tất cả những gì mà người dùng sẽ nhìn thấy - như trình duyệt web và các tập tin - được xem là *không gian người dùng*. Những application này sẽ tương tác với kernel thông qua một system call interface (SCI).

  *Nghĩ như thế này*: Kernel là một trợ lí cá nhân rất bận rộn cho một người điều hành quyền lực (phần cứng). Và nhiệm vụ của trợ lí cá nhân là chuyển tiếp các tin nhắn và yêu cầu (từ process) từ các nhân viên và những người bên ngoài (người dùng) đến người điều hành, để biết rằng cái gì được lưu ở đâu (bộ nhớ), và xác định xem ai có quyền liên lạc với người điều hành vào lúc nào và trong bao lâu.

  ### Kernel làm gì bên trong OS
  Để đem kernel vào ngữ cảnh này, chúng ta có thể xem một OS Linux có 3 layer chính:

  - **Phần cứng**: Máy chủ vật lí - nằm cuối cùng hoặc là nền của hệ thống, tạo nên bởi bộ nhớ (RAM) và các bộ xử lí hay đơn vị xử lí trung tâm (CPU), cũng như là các thiết bị có input/output như *thiết bị lưu trữ*, *mạng* và *đồ họa*. CPU sẽ thực hiện việc tính toán và đọc từ/viết vào bộ nhớ.
  - **Linux Kernel**: Hạt nhân của OS (Nằm ở giữa). Nó là phần mềm nằm trong bộ nhớ mà sẽ cho biết CPU cần phải làm gì.
  - **User process**: Là các chương trình đang chạy sẽ được kernel quản lí. User process là những gì sẽ tạo nên *không gian người dùng*. Kernel cũng cho phép các process này và server giao tiếp với nhau (còn được gọi là inter-process communication hay IPC).
  
  Code được thực thi bởi hệ thống khi chạy trên CPU sẽ ở một trong hai chế độ: *Kernel mode* hoặc *user mode*. Code chạy ở *kernel mode* có quyền truy cập không bị hạn chế đối với các thiết bị phần cứng, trong khi đó code chạy ở *user mode* sẽ bị quyền truy cập hạn chế hơn vào CPU và bộ nhớ thông qua SCI (System call interface). Sự phân biệt tương tự cũng áp dụng cho bộ nhớ (giữa không gian kernel và không gian người dùng). 

  Điều này cũng có nghĩa là nếu một process failed ở user mode, thiệt hại sẽ được hạn chế và có thể được phục hồi thông qua kernel. Tuy nhiên, bởi quyền truy cập của nó vào các bộ xử lí và bộ nhớ, kernel process crash có thể kéo theo sập toàn bộ hệ thống. Vì có sẵn các biện pháp bảo vệ và các quyền cần thiết để vượt qua ranh giới nên sự cố trong quy trình của người dùng thường không thể gây ra quá nhiều vấn đề.
  
  </details>

- <details>
  <summary><b>What is Shell?</b></summary>

  [Link bài viết gốc](https://gnu.org/software/bash/manual/html_node/What-is-a-shell_003f.html)

  ### Khái niệm
  Về cơ bản, shell chỉ đơn giản là một bộ xử lí macro (macro processor) dùng để thực thi các lệnh. Định nghĩa *macro processor* nghĩa là một chức năng mà tại đó các văn bản và kí hiệu được mở rộng ra để tạo thành các biểu thức lớn hơn.

  Unix shell vừa là trình thông dịch lệnh, vừa là ngôn ngữ lập trình. Với việc là trình thông dịch lệnh, shell cung cấp một giao diện người dùng với các tiện ích GNU phong phú. Với việc là một ngôn ngữ lập trình, các tiện ích của shell có thể được kết hợp với nhau. Các tập tin chứa các lệnh có thể được tạo ra, và bản thân tập tin đó trở thành một lệnh. Những lệnh mới này có trạng thái giống với các lệnh hệ thống trong các thư mục `/bin`, cho phép người dùng hoặc nhóm người dùng có thể thiết lập các môi trường tùy chỉnh để tự động hóa các common task.

  Shell có thể được sử dụng dưới dạng tương tác hoặc không tương tác. Trong chế độ tương tác, chúng nhận một input được nhập vào từ bàn phím. Khi thực thi ở chế độ không tương tác, shell thực thi lệnh đọc được từ một file.

  Một shell cho phép thực thi các lệnh GNU, theo hướng đồng bộ hoặc bất đồng bộ. Shell chờ đợi các lệnh đồng bộ được hoàn thành trước khi nhận thêm input; các lệnh bất đồng bộ thì tiếp tục hoạt động một cách song song với shell trong khi nó đọc và thực thi các lệnh khác. Cấu trúc *chuyển hướng* cho phép kiểm soát chi tiết input và output của các lệnh. Hơn nữa, shell cho phép kiểm soát nội dung của môi trường dòng lệnh.

  Shell chấp nhận các lệnh có thể đọc được từ người dùng và chuyển đổi chúng thành thứ mà kernel có thể hiểu được.

  ![img](images/module-06/f1543025-339d-43f9-948a-ebb559f16cb2.webp)

  **Shell** được chia làm hai loại: *Command Line Shell* và *Graphical shell*.

  ### Command Line Shell
  **Shell** có thể được truy cập bởi người dùng bằng cách sử dụng **command line interface**. Một chương trình đặc biệt có tên **Terminal** trong Linux được cung cấp để nhập vào các lệnh có thể đọc được của người dùng như "cat", "ls", và sau đó nó được thực thi. Kết quả sau đó sẽ được hiển thị lên **Terminal**

  ### Graphical Shell
  - **Graphical Shell** cung cấp phương tiện để thao tác với các chương trình dựa trên graphical user interface (GUI), bằng cách cho phép các hoạt động như **open**, **close**, **move** và **resize window**, cũng như chuyển trọng tâm giữa các cửa sổ.
  - Window OS hoặc Ubuntu OS có thể được coi là ví dụ điển hình cung cấp GUI cho người dùng để tương tác với chương trình. Người dùng không cần nhập lệnh cho mọi hành động.
  - Một số **shell** có sẵn trong các hệ thống Linux:
    - BASH (Bourne Again Shell) - Được sử dụng rộng rãi nhất trong các hệ thống Linux. Nó được sử dụng làm vỏ đăng nhập mặc định trong Linux / MacOS. Nó cũng có thể cài đặt trên Window OS.
    - CSH (C Shell) - Cú pháp và cách sử dụng của **C Shell** rất giống với ngôn ngữ lập trình C.
    - KSH (Korn Shell) - Korn Shell cũng là cơ sở cho các thông số kỹ thuật tiêu chuẩn của POSIX Shell, vv...
  - Mỗi shell thực hiện cùng một công việc nhưng hiểu các lệnh khác nhau và cung cấp các hàm dựng sẵn khác nhau.

  </details>

- <details>
  <summary><b>Schell Script?</b></summary>

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

  </details>

- <details>
  <summary><b>Schell Script - Varriables & Basic Operators</b></summary>

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
  
  </details>
- <details>
  <summary>
  <b>Schell Programming - If..else, Array, Loops, Function, ...</b>
  </summary>

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
  </details>
  
</details>
<details>
<summary>
<b>Module 7 - Networking</b>
</summary>

1. **[Difference Network Modes in VMWare](module-07/network-modes-in-vm.md)**
  
2. **[Network Configuration Files in Linux](module-07/network-configuration-files.md)**

3. **[Predictable Consistent Network Device Naming](module-07/network-predictable.md)**

4. **[Managing IP Address with ip command](module-07/ip-address-managing-with-ip-command.md)**
</details>
<details>
<summary>
<b>Sub Module 1 - OS Refresher</b>
</summary>

1. **[Introduction of process management](s-module-01/introduction-process-management.md)**

2. **[Introduction of process synchronization](s-module-01/introduction-process-synchronization.md)**
  
3. **[Thread in OS](s-module-01/thread-in-os.md)**
</details>

<details>
<summary>
<b>Sub Module 2 - Network Refresher</b>
</summary>

1. **[Networking Fundamentals - Hosts, IP Addresses, Networks](s-module-02/hosts-ip-networks.md)**
  
2. **[Network Devices - Hub, Bridge, Switch, Router](s-module-02/hub-bridge-switch-router.md)**
   
3. **[OSI Model In Practical Perspective - L1, L2, L3](s-module-02/osi-practical-perspective.md)**

4. **[OSI Model In Practical Perspective - L4](s-module-02/osi-practical-perspective-2.md)**
   
5. **[What is OSI model](s-module-02/what-is-osi-model.md)**
</details>