# 11. join và split

Lệnh `join` sẽ giúp chúng ta join hai file với nhau bằng một trường nào đó. Hãy giả sử chúng ta có hai file muốn join với nhau:

```sh
file1.txt
1 John
2 Jane
3 Mary

file2.txt
1 Doe
2 Doe
3 Sue


$ join file1.txt file2.txt
1 John Doe
2 Jane Doe
3 Mary Sue
```

Bạn có thể thấy cách mà hai file đã join với nhau?

:bulb: Lệnh này join các file với nhau bằng trường đầu tiên theo mặc định và trường phải giống hệt nhau.

Thế giả sử muốn join hai file sau lại với nhau thì sao?

```sh
file1.txt
John 1
Jane 2
Mary 3


file2.txt
1 Doe
2 Doe
3 Sue
```

Để join hai file này thì chúng ta cần chỉ định rõ là cần join theo trường nào, trong trường hợp này chúng ta muốn trường thứ 2 của file1.txt join với trường 1 của file2.txt. Lệnh sẽ trông như sau:

```sh
$ join -1 2 -2 1 file1.txt file2.txt
1 John Doe
2 Jane Doe
3 Mary Sue
```

`-1` đại diện cho file đầu tiên và `-2` đại diện cho file tiếp theo, khá là dễ hiểu.

Ngoài ra bạn cũng có thể chia nhỏ một file ra thành nhiều file với lệnh `split`.

```sh
$ split somefile
```

:bulb: Lệnh này sẽ chia nhỏ file ra, theo mặc định thì file sẽ bị chia nhỏ ra khi đạt tới giới hạn 1000 dòng. File mới tạo ra sẽ có tên là x** theo mặc định.