# 8. head

Nếu chúng ta có một file có nội dung rất rất dài, như `/var/log/syslog`, nhưng chúng ta chỉ muốn đọc vài dòng văn bản đầu tiên thì sao? Lệnh `head` được sinh ra cho mục đích này.

```sh
$ head /var/log/syslog
```

Mặc định thì lệnh này xem 10 dòng đầu tiên của file, chúng ta có thể thay đổi số lượng dòng bằng flag `-n`.

```sh
$ head -n 15 /var/log/syslog
```