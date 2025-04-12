# 10. expand và unexpand

Trong phần [6. cut](6-cut.md), chúng ta đã có một file sample.txt mà nội dung có chứa kí tự tab. Thông thường thì tab là đủ để thể hiện sự khác biệt nhưng trong một số file văn bản thì có thể là chưa đủ. Để thay đổi kí tự tab thành khoảng trắng, dùng lệnh `expand`.

```sh
$ expand sample.txt
```

:bulb: Lệnh trên sẽ in ra output của file sample.txt với nội dung mà trong đó các dấu tab sẽ bị thay thế bằng khoảng trắng.

Để lưu lại nội dung phiên bản đã qua sửa đổi này thì có thể sử dụng toán tử điều hướng.

```sh
$ expand sample.txt > result.txt
```

:bulb: Trái ngược với lệnh `expand`, chúng ta có thể in ra phiên bản chuyển đổi từ khoảng trắng sang tab bằng lệnh `unexpand`

```sh
$ unexpand -a result.txt
```

