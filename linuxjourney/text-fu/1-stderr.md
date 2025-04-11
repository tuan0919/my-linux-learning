# 3. stderr (Standard Error)

Chà, bây giờ hãy thử một thứ gì đó khác biệt nhé, hãy thử liệt kê nội dung của một thư mục không tồn tại rồi chuyển hướng đầu ra của nó đến file peanuts.txt lần nữa.

```sh
$ ls /fake/directory > peanuts.txt 
```

Kết quả của lệnh này đại loại sẽ là:

```sh
ls: cannot access /fake/directory: No such file or directory
```

Có thể bạn sẽ nghĩ "Ồ, thế thì nội dung file peanuts.txt lúc này chắc hẳn lẽ là message trên". Thế nhưng không phải đâu :smiley:. 

:bulb: Thực ra tại đây có thêm một luồng I/O khác hoạt động nữa, thằng này gọi là standard error (stderr).

:bulb: Mặc định, stderr cũng trả kết quả đến màn hình, nhưng kết quả của nó sẽ là kết quả lỗi, thế nên message lỗi phía trên sẽ được gửi đến stderr.

Thế nên, để có kết quả lỗi trong file peanuts.txt, chúng ta sẽ phải điều hướng luôn stderr. Cơ mà, toán tử để điều hướng sẽ không phải là `<` hay `>` đâu.

Mà chúng ta sẽ dùng đến một khái niệm gọi là file descriptor :dizzy_face:. Một file descriptor về cơ bản là một số không âm được sử dụng để truy cập vào một file hay một luồng. Chúng ta sẽ đi chi tiết khái niệm này sau

Hiện tại thì chúng ta sẽ chỉ cần biết file descriptor cho stdin, stdout và stderr lần lượt là 0, 1 và 2.

Vậy, để điều hướng stderr, chúng ta sử dụng toán tử `2>`

```sh
$ ls /fake/directory 2> peanuts.txt
```

Lúc này bạn sẽ thấy nội dung lỗi nằm trong file peanuts.txt.

Thế nếu tôi muốn thấy cả stderr và stdout bên trong file này thì phải làm sao? Điều này cũng khả thi với file descriptor:

```sh
$ ls /fake/directory > peanuts.txt 2>&1
```

Lệnh này chuyển hướng kết quả lệnh `ls /fake/directory` vào file peanuts.txt cũng như chuyển hướng stderr đến stdout thông qua `2>&1`. 

:collision: Thứ tự gõ các toán tử này sẽ khá quan trọng, bởi vì `2>&1` sẽ chuyển hướng stderr đến nơi mà stdout đang trỏ đến.

:collision: Trong trường hợp này, do stdout đang trỏ đến peanuts.txt, cho nên `2>&1` sẽ chuyển hướng stderr đến file peanuts.txt.

Mở file peanuts.txt ra và bạn sẽ thấy kết quả của cả stdout và stderr nằm trong đó!

Có cách viết ngắn gọn hơn như sau:

```sh
$ ls /fake/directory &> peanuts.txt
```

Vậy trường hợp tôi cóc thèm quan tâm đến mesasge được trả ra tại stderr mà muốn vứt nó sang một bên thì sao? Vậy thì bạn có thể chuyển hướng stderr đến một file đặc biệt là `/dev/null`, file này cho phép hủy bỏ tất cả đầu vào của nó.

```sh
$ ls /fake/directory 2> /dev/null
```