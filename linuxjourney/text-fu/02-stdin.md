# 2. stdin (Standard In)

Trong phần trước, chúng ta đã đề cập đến việc chúng ta có nhiều luồng [đầu ra mặc định](stdout.md) để có thể thao tác. Thì tương tự, chúng ta cũng có nhiều luồng đầu vào mặc định (stdin). 

Chúng ta đã biết rằng luồng stdin có thể đến từ bàn phím, ngoài ra nó còn có thể đến từ các nguồn khác như là một file, một đầu ra của tiến hình khác hay thậm chí là của một terminal, hãy xem xét một ví dụ.

Hãy dùng lại file peanuts.txt từ phần trước trong ví dụ này, nhớ rằng trong file này sẽ có chứa chữ Hello World bên trong nhé :eyes:.

```sh
$ cat < peanuts.txt > banana.txt 
```

Như cái cách ta dùng toán tử `>` để chuyển hướng stdout, thì giờ ta dùng toán tử `<` để chuyển hướng stdin.

Thông thường thì trong lệnh `cat`, chúng ta truyền một file vào nó thì file đó sẽ trở thành stdin, trong trường hợp này thì file peanuts.txt sẽ là stdin.

Sau đó, output của lệnh `cat peanuts.txt`, tức dòng chữ Hello World lại được định hướng stdout đến một file mới là banana.txt.