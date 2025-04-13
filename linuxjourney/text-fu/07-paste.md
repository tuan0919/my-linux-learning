# 7. paste
Lệnh `paste` tương tự với lệnh `cat`, nó sẽ gộp nhiều dòng vào một file. Hãy tạo một file với nội dung sau:

```sh
sample2.txt

The

quick

brown

fox
```

Để gộp tất cả các dòng này thành một dòng duy nhất:

```sh
$ paste -s sample2.txt
```

Kí tự phân cách mặc định trong lệnh `paste` là TAB, thế nên kết quả của lệnh trên là một dòng với kí tự TAB nằm giữa mỗi từ.

Hãy chuyển kí tự delimeter mặc định (-d) thành kí tự có tính phổ biến hơn:

```sh
$ paste -d ' ' -s sample2.txt
```

Giờ thì các từ sẽ cách nhau bằng khoảng trắng.