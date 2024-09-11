## Giới thiệu về quyền truy xuất:
Quyền là thuộc tính của một tệp và thư mục. Nó cho biết từng đối tượng người dùng (chủ sở hữu, người cùng nhóm, người dùng khác) có quyền gì trên một tệp và thư mục. Linux sử dụng 9 bit cho việc này, trong đó 3 bit đầu cho biết quyền đọc, ghi, thực thi của owner, 3 bit tiếp theo cho biết quyền của group, 3 bit cuối cho biết quyền của other. Trong các lệnh, 3 bit xác định quyền cho một đối tượng người dùng được biểu diễn bằng một số nguyên (có giá trị từ 0 đến 7), quyền được biểu diễn bằng ba số nguyên liên tiếp.

| Number | Permission Type | Symbol |
|:------:|:---------------:|:------:|
| 0 | No Permission | - |
| 1 | Execute | --x |
| 2 | Write | -w- |
| 3 | Execute + Write | -wx |
| 4 | Read | r-- |
| 5 | Read + Execute | r-x |
| 6 | Read + Write | rw- |
| 7 | Read + Write + Execute | rwx |

## Quyền cho tệp và thư mục được tạo mới:
Với các tệp và thư mục được tạo mới, quyền được xác định dựa trên quyền cơ sở (base permission) và user mask.

Base permission được thiết lập sẵn và không thể thay đổi.

- Đối với file thông thường thì BS là 666 (`rw-rw-rw`)
- Đối với thư mục (file đặc biệt) thì BS là 777 (`rwxrwxrwx`)

Có thể tính nhanh quyền truy xuất tệp và thư mục theo các công thức sau:

```
Quyền truy cập file = 666 - unmask
Quyền truy cập folder = 777 - unmask
```

Giá trị user mask mặc định cho người dùng thông thường là **002**

Với mask này thì quyền hạn truy cập mặc định cho thư mục là **775** và file là **664**

Giá trị mask mặc định cho root là **022**

Với mask này thì quyền hạn truy cập mặc định cho thư mục là **755** và file là **644**

Sử dụng chương trình **umask** để thay đổi user mask. **Các tệp và thư mục được tạo ra sau lệnh umask sẽ chịu tác động của giá trị mask mới**.

## Thay đổi quyền của tệp và thư mục đã tồn tại:

Có thể sử dụng chương trình **umask** để thay đổi user mask, sau đó dùng chương trình touch để cập nhật quyền của tệp theo user mask mới . Dưới đây là một ví dụ minh họa việc giá trị user mask quyết định các quyền hạn trên file.txt như thế nào.

```sh
unmask 077
touch test_file.txt
ls-l test_file.txt

> -rw------ 1 uit uit 0 2024-08-20 11:10 test_file.txt
```

Note: *Cơ chế làm việc của umask khiến chúng ta không thể tạo ra các file với quyền execute. Vì Base permission của file luôn là 666, tức các bit ứng với quyền execute đều bằng 0, nên bất kể giá trị mask bằng bao nhiêu thì quyền của file đều không có execute.*

Cách khác để thay đổi quyền của tệp và thư mục đã tồn tại là sử dụng chmod. Sử dụng chmod có thể thêm quyền thực thi cho tệp và thư mục.

`chmod [OPTION] MODE FILE`

trong đó:
- OPTION hay được dùng nhất là -R hoặc --recursive (đệ quy) khi muốn áp dụng quyền cho tất cả tệp và các thư mục con.
- MODE cho biết đối tượng người dùng nào (u: user sở hữu; g: group; o: other, a: all) được cấp/thu hồi/gán (+-=) quyền gì (rwxXst hoặc [0-7]+)
- File là file hoặc folder bạn muốn thay đổi quyền

## Thay đổi chủ sở hữu của tệp và thư muc
Người tạo ra tệp hay thư mục là chủ sở hữu (owner) mặc định của tệp hay thư mục. Quyền sở hữu của tệp hay thư mục còn thuộc owning group. Owner hoặc root có thể thay đổi chủ sở hữu của tệp và thư mục bằng dùng chương trình chown.

`chown [OPTION] [OWNER][:[GROUP]] FILE`

## SUID, SGID, Sticky bit
Ngoài 9 bits cơ bản xác định các quyền rwx của owner, group và other, Linux sử dụng 3 bit khác để định nghĩa quyền trên tệp và thư mục. Các bit này lần lượt là SUID, SGID, Sticky. Trong các lệnh, một số nguyên nữa có giá trị từ 0 đến 7 được dùng để xác định ba quyền này. Ví dụ, trong lệnh

```sh
chmod 6750 file1.txt
```
số 6 (nhị phân là 110) **đầu tiên** trong quyền xác định SUID, SGID được bật, sticky không được bật.

Ý nghĩa của ba bit SUID, SGID, Sticky được giải thích lần lượt như sau.

## SUID (Set owner User ID up on execution)
Thông thường, khi một chương trình/tệp/lệnh chạy, nó sử dụng các quyền của người dùng hiện tại, hay người dùng chạy nó. Nếu SUID được đặt, chương trình sẽ sử dụng quyền của owner chứ không phải quyền của người dùng hiện tại. Ví dụ, owner của /etc/passwd, /etc/shadow là root. Người dùng thông thường không có quyền ghi các tệp này. Nếu các tệp này không được đặt quyền SUID, khi người dùng chạy lệnh passwd sẽ xuất hiện lỗi do không mở và ghi vào tệp /etc/shadow được. Ngược lại, khi các tệp này được đặt quyền SUID, người dùng thông thường cũng có thể chạy lệnh passwd.

Ví dụ:
- Đặt quyền SUID của tệp cho người dùng hiện tại: `chmod u+s file1.txt` hoặc `chmod 4750 file1.txt`
- Bỏ quyền SUID của tệp đối với người dùng hiện tại: `chmod u-x file1.txt`

Khi SUID được bật, bit x của owner được hiển thị là s nếu owner có quyền thực thi . Nếu owner không có quyền thực thi, bit x của owner được hiển thị là S. Ví dụ, -rwSrw-r-- có nghĩa là bit SUID đã được bật nhưng bit x của owner không được bật, -rwsrw-r-- có nghĩa là bit SUID đã được bật và bit x của owner được bật, rwxrw-r-- nghĩa là bit SUID không được bật và owner có quyền thực thi.

## SGID (Set Group ID up on execution)
Tương tự SUID, nhưng thay owner là group. Nếu SGID được đặt, chương trình sẽ sử dụng quyền của group, chứ không phải quyền của người dùng hiện tại.

Ví dụ:
- Đặt quyền SGID cho tệp `chmod g+s file.txt` hoặc `chmod 2750 file.txt`

Khi SGID được bật, bit x của group được hiển thị là s nếu group có quyền thực thi. Nếu group không có quyền thực thi, bit x của group được hiển thị là S. Ví dụ, -rwxrwSr-- có nghĩa là bit SGID đã được bật nhưng bit x của group không được bật, -rwxrwsr-- có nghĩa là bit SGID đã được bật và bit x của group được bật, rwxrwxr-- nghĩa là bit SGID không được bật và owner có quyền thực thi.

## Sticky bit
Sticky bit áp dụng cho thư mục. Nếu bit này được bật, chỉ owner và root có thể xóa nội dung của thư mục. Sử dụng bit này để thiết lập cấu hình ngăn người dùng xóa dữ liệu của người khác.

Ví dụ:
- Bật sticky bit trên thư mục /important: `chmod o+t /important` hoặc `chmod +t /important` hoặc `chmod 1757 /important`
- Tắt sticky bit trên thư mục /lab: `chmod o-t /lab`

Khi sticky được bật, bit x của other được hiển thị là t nếu other có quyền thực thi. Nếu other không có quyền thực thi, bit x của other được hiển thị là T. Ví dụ, -rwxrw-r-T có nghĩa là sticky đã được bật nhưng bit x của other không được bật.