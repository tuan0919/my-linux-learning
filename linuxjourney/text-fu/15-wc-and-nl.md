# 15. wc and nl

Lệnh `wc` (wordcount) sẽ cho biết số lượng các từ nằm trong một file.

```sh
$ wc /etc/passwd
96     265    5925 /etc/passwd
```

:bulb: Kết quả hiện ra lần lượt là:

```sh
[số_dòng] [số_từ] [số_bytes].
```

Nếu bạn chỉ quan tâm đến vài thông tin bên trên thì có thể dùng các flag tương ứng lần lượt là: `-l`, `-w`, `-c`.

```sh
$ wc -l /etc/passwd
96
```

Một lệnh khác cũng cho phép bạn kiểm tra số dòng trong một file là lệnh `nl` (number line):

```sh
file1.txt
i
like
turtles

$ nl file1.txt
1. i
2. like
3. turtles
```