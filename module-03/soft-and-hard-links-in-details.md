# Một số khái niệm cần biết

Trong hệ thống file Linux, một liên kết (link) là một kết nối giữa file name và dữ liệu thực tế trên disk.

Có hai loại liên kết chính có thể được tạo: "hard" links, và "soft" hay symbolic links. Trước khi tìm hiểu về hard links và symbolic links, có một khái niệm khác cần hiểu rõ là “inode” - một khái niệm cơ bản trong Linux filesystem. Mỗi đối tượng của filesystem được đại diện bởi một inode.

# Inode
Trong Linux, dữ liệu của các file được chia thành các block. Có nhiều cách tổ chức để liên kết các khối dữ liệu trong một file với nhau, một trong các cách đó là dùng chỉ mục (indexed allocation).

![alt text](/images/123213218SDHUASHDUS.png)

Trong một inode có các metadata sau:
- Dung lượng file tính bằng bytes.
- Device ID : id của thiết bị lưu file.
- User ID : id chủ sở hữu của file.
- Group ID: id nhóm của chủ sở hữu file.
- File mode : gồm kiểu file và cách thức truy cập file.
- Timestamps: các mốc thời gian khi: bản thân inode bị thay đổi (ctime, inode change time), nội dung file thay đổi (mtime, modification time) và lần truy cập mới nhất (atime, access time).
- Link count : số lượng hard links trỏ đến inode. Các con trỏ chỉ đến các blocks trên ổ cứng dùng lưu nội dung file. Các con trỏ cho biết file nằm ở đâu để đọc nội dung.
- ...

>Inode là một cấu trúc dữ liệu trong hệ thống tệp truyền thống của các họ Unix ví dụ như UFS hoặc EXT3. Inode lưu trữ thông tin về 1 tệp thông thường, thư mục, hay những đối tượng khác của hệ thống tệp tin.

Có hai chú ý trong nội dung inode:
- Inode không chứa tên file, thư mục.
- Các con trỏ là thành phần quan trọng nhất: nó cho biết địa chỉ các block lưu nội dung file và tìm đến các block đó có thể truy cập được nội dung file.

# Hard Link
Hard Link là các liên kết cấp thấp (low-level links) mà hệ thống sử dụng để tạo các thành phần chính hệ thống file, chẳng hạn như file và thư mục. Liên kết cứng sẽ tạo ra một liên kết trong cùng hệ thống tập tin với 2 inode entry tương ứng trỏ đến cùng một nội dung vật lí (cùng số inode vì chúng trỏ đến cùng dữ liệu).

Tất cả các hệ thống tệp tin dựa trên thư mục phải có ít nhất một liên kết cứng (link counts từ 1 trở lên) cung cấp tên gốc cho mỗi tệp tin.

![alt text](/images/SDADUIJSA.png)

# Symbolic Link
- Hầu hết người dùng không muốn tự tạo hoặc sửa đổi các hard links, nhưng các symbolic links là một công cụ hữu ích cho bất kỳ người dùng Linux nào.
- **Symbolic links** là một file đặc biệt trỏ đến một file hoặc thư mục khác - được gọi là target. Khi được tạo, một symbolic links có thể được sử dụng thay cho target file. Nó có thể có một tên độc nhất, và được đặt trong bất kỳ thư mục nào. Nhiều symbolic links thậm chí có thể được tạo cho cùng một target file, cho phép truy cập target bằng nhiều tên khác nhau.

![alt text](/images/sDSAASD.png)

- Symbolic link không chứa bản sao dữ liệu của target file. Nó tương tự như một shortcut trong Microsoft Windows: nếu bạn xóa một symbolic link, target sẽ không bị ảnh hưởng. Vì chỉ đơn thuần là một shortcut, symbolic link không dùng đến inode entry. Nó sẽ tạo ra một inode mới và nội dung của inode này trỏ đến tên tập tin gốc.
- Ngoài ra, nếu target của một symbolic link bị xóa, di chuyển hoặc đổi tên, symbolic link không được cập nhật. Khi điều này xảy ra, liên kết tượng trưng được gọi là "broken" hoặc "orphaned" và sẽ không còn hoạt động như một liên kết.

Lệnh:
- `ln`: tạo hard link.
- `ln -s`: tạo soft link.

![img](/images/saidjsadsad1273111.png)