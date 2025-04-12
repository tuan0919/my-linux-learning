# 9. tail

Tương tự lệnh `head` nhưng trái ngược, thì thằng `tail` này cho phép chúng ta đọc 10 dòng cuối của một file.

```sh
$ tail /var/log/syslog
```

Tất nhiên bạn cũng có thể thay đổi số lượng dòng với flag `-n`

```sh
$ tail -n 10 /var/log/syslog
```

Một tùy chọn khác khá hay là flag `-f` (follow), tùy chọn này cho phép theo dõi tập tin khi mà nó mở rộng hơn

```sh
$ tail -f /var/log/syslog
```

Tập tin syslog sẽ liên tục thay đổi mỗi khi chúng ta tương tác với hệ điều hành, lệnh trên sẽ cho ta thấy tất cả mọi thứ vừa được thêm vào file đó.