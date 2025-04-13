# 4. pipe and tee

Bây giờ chúng ta sẽ tìm hiểu một tí về hệ thống ống nước :satisfied:, không hẳn theo nghĩa đen nhưng cũng đại loại là thế. Đầu tiên thử chạy lệnh sau:

```sh
$ ls -la /etc
```

Chạy xong là bạn sẽ thấy rất nhiều kết quả hiện ra, và thật sự khá là khó đọc, chẳng phải sẽ tiện hơn nếu chúng ta đem các kết quả này và hiển thị trong một lệnh khác như `less`? Thật ra là được đấy:

```sh
$ ls -la /etc | less
```

:bulb: Toán tử `|` là toán tử pipe (đường ống), nó sẽ cho phép chúng ta lấy stdout của một lệnh và biến nó trở thành stdin của lệnh khác.

:bulb: Trong trường hợp này, chúng ta đang lấy stdout của `ls -la /etc` và bỏ vào nối ống nó vào lệnh `less`, toán tử pipe cực kỳ hữu ích và chúng ta sẽ dùng nó rất nhiều.

Thế trong trường hợp chúng ta muốn trả kết quả ra hai stream khác nhau thì sao? Linux cũng hỗ trợ luôn mong muốn này với lệnh `tee`

```sh
$ ls | tee peanuts.txt
```

Khi chạy lệnh này, bạn sẽ thấy kết quả của lệnh `ls` vừa nằm trong file peanuts, vừa hiển thị ra màn hình.
