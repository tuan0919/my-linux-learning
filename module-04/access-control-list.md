ACLs là cách khác để xác định quyền trên tệp và thư mục. Chúng cho phép gán quyền cho một người dùng hoặc một nhóm bất kỳ, thậm chí không tương tác với owner hoặc owning group. ACLs hỗ trợ các hệ thống file `ReiserFS`, `Ext2`, `Ext3`, `JFS`, `XFS`. Một tệp hoặc thư mục có thể có nhiều ACL.

Dùng ls -dl để kiểm tra quyền:

```sh
$ ls -dl mydir/
> drwxr-xr-x 2 quanta quanta 4096 2007-12-29 22:53 mydir/

```

Kiểm tra trạng thái khởi đầu của ACL:

```sh
$ getfacl mydir/
# file: mydir
# owner: quanta
# group: quanta
user::rwx
group::r-x
other::---
```

Gán quyền đọc, ghi, thi hành cho user nqat0919 và group friends:

```sh
$ setfacl -m user:nqat0919:rwx,group:friends:rwx mydir/
```

Tùy chọn **-m** sẽ nhắc setfacl chỉnh sửa một ACL đã tồn tại.

Xem lại ACL với lệnh **getfacl**:

```sh
$ getfacl mydir/
# file: mydir
# owner: quanta
# group: quanta
user::rwx
user:nqat0919:rwx
group::r-x
group:friends:rwx
mask::rwx
other::---
```

Ngoài các mục (entries) cho user nqat0919 và group friends, mask entry cũng được tạo ra. mask định nghĩa quyền truy cập có hiệu lực lớn nhất cho tất cả các entries của group.

Bây giờ thử dùng chmod để bỏ quyền write của group, output của lệnh ls cho thấy mask bits đã được điều chỉnh với chmod:

```sh
$ sudo chmod g-w mydir/
$ getfacl mydir/
# file: mydir
# owner: quanta
# group: quanta
user::rwx
user:nqat0919:rwx                  #effective:r-x
group::r-x
group:friends:rwx               #effective:r-x
mask::r-x
other::---
```

Default ACLs Default ACL ảnh hưởng đến các thư mục con cũng như là các files. Nói cách khác, các thư mục con và tệp kế thừa default ACL của thư mục cha.

Ví dụ thực tế:

Giả sử /public là thư mục dùng chung cho mọi người trong công ty, hãy thiết lập để sao cho bất kỳ ai thuộc bất kỳ nhóm nào cũng có khả năng đọc file va chuyển vào trong thư mục này nhưng chỉ có người dùng trong nhóm quantri mới có thể ghi vào các file trong thư mục này.

```sh
setfacl -d --set u::rx,g::rx,o::rx,g:quantri:rwx,m:rwx /pulbic
getfacl /public
```