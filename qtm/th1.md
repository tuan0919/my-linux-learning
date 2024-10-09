## Đề bài:

### Phần I
1. Thêm một harddisk kiểu scsi dung lượng 2GB vào hệ thống
2. Tạo partition trên đĩa cứng mới
3. Định dang filesystem ext3 cho partition mới
4. Mount tự động parttion mới vao hệ thống vơi mount point là /home
5. Tạo các user mới là user1, user2 password tùy ý
### Phần II
1. Lệnh ls [-laid]
2. Lệnh cat, touch, echo
3. Lệnh cp, rm [-rif]
Tạo thư mục /tmp/source trong đó có các thư mục con t1,t2 và các thư mục con t11, t12,
t21, t22. Trong mỗi thư mục có một số file.
- Viết lệnh copy toàn bộ cấu trúc thư mục /tmp/source vào trong thư mục
/tmp/dest cho 2 trường hợp trong dest có thư mục con source và trong dest
không có thư mục con source
- Viết lệnh copy để chỉ copy các file nằm ngay trong /tmp/source (không bao gồm
thư mục con) vào trong /tmp/dest
- Thay đổi các option để khi copy luôn hiển thị hộp thoại hoặc không bao giờ hiển
thi hộp thoại khi file đích đã tồn tại
- Copy như là link
4. Link: Hard link và soft link
- Dùng touch hoặc echo tạo file abc có nội dung là quan tri mang. Kiểm tra
quyền hạn, chủ nhân, inode number và số hard link bằng lệnh ls.
- Tạo 2 hard link là abch1 và abch2. Kiểm tra quyền hạn, chủ nhân, inode number
và số hard link bằng lệnh ls.
- Tạo soft link là abcs. Kiểm tra quyền hạn, chủ nhân, inode number và số hard
link bằng lệnh ls.
- Chown, chmod rồi kiểm tra lại quyền hạn, chủ nhân trên original, hard link và
soft link
- Xoá file abc. kiểm tra các liên kết
- Tạo lại file abc với nội dung Bai thuc hanh so 1. Kiểm tra nội dung hard và soft
link
- Xoá file abc, ghi dữ liệu vào softlink abcs sau đó tạo lại file abc với nội dung
thuc hành voi lien ket. Kiểm tra nội dung hard và soft link
5. Thực hành các lệnh useradd, usermod, userdel, su, tạo user có quyền của root
6. Thực hành các lệnh groupadd, groupmod, groupdel, id, gpaaswd
7. Thực hành các lênh chmod, kiểm tra sticky bit và hiệu ứng của nó
8. Dùng các lệnh locate , find, ls + grep dùng để tìm file

## Bài làm
### Phần I

#### 1. Thêm một harddisk kiểu scsi dung lượng 2GB vào hệ thống:
- Sau khi đã cài xong **hardisk** kiểu **scsi** vào hệ thống thì boot hệ điều hành lên, đăng nhập với quyền root.

#### 2. Tạo partition trên đĩa cứng mới
- Kiểm tra thông tin ổ đĩa scsi vừa gắn vào bằng lệnh `lsblk`:

  ![img](/images/qtm/VirtualBox_Centos%207_10_09_2024_01_11_01.png)
  
  *Đã thêm thành công ổ cứng mới có tên `sdb` vào*

- Thực hiện phân vùng cho ổ  `/dev/sdb` với lệnh `fdisk /dev/sdb`:
  - **m** - Hiện menu.
  - **n** - Tạo phân vùng mới.
  - **p** - Chọn loại partiton **primary**
  - **Enter** - Chọn sector bắt đầu, thường là 2048
  - **+2G** - Nhập kích thước partition này là 2gb cho đúng đề bài nếu hard disk add vào lớn hơn (5gb).
  - **w** - write table và thoát
  
  ![img](/images/qtm/VirtualBox_Centos%207_10_09_2024_01_18_17.png)

- Kiểm tra thông tin partition vừa tạo với lệnh `lsblk`, Thấy được `sdb` có một partiton là `sdb1` là thành công.
#### 3. Định dang filesystem ext3 cho partition mới

- Sử dụng lệnh `mkfs -t ext3 /dev/sdb1` (make file system) để chỉ định ext3 làm file systesystemctl restart network
  - Thêm dòng này vào:
  
  ```sh
  /dev/sdb1 /homesystemctl restart network   ext3    defaults    1   1
  ```

  ![img](/images/qtm/VirtualBox_Centos%207_10_09_2024_01_33_39.png)

  - Dùng lệnh `mount -a`.
  - Kiểm tra bằng `lsblk`, nếu thấy mount point của `sdb1` là `/home` thì thành công.

### 5. Tạo các user mới là user1, user2 password tùy ý
```sh
useradd user1
useradd user2
passwd user1
passwd user2
```

