# File System Structure của Linux:

- `/boot`: chứa file được sử dụng bởi bootloader (grub.cfg).
- `/root`: thư mục home của user root.
- `/dev`: System devices (eg disk, cdroom, speakers, flashdrive, keyboard etc)
- `/etc`: Configuration files.
- `/bin -> /usr/bin`: Everyday user commands.
- `/sbin -> /usr/sbin`: System/filesystem commands.
- `/opt`: optional addons applications (các apps không thuộc về OS).
- `/proc`: Chứa các file, thư mục cho các process đang chạy (bị xóa khi shutdown).
- `/lib -> /usr/lib`: các file thư viện được viết bằng C cần thiết cho các commands hoặc apps.
- `/tmp`: thư mục chứa các file tempory.
- `/home`: thư mục home của user.
- `/var`: logs của hệ thống.
- `/run`: các daemons hệ thống chạy rất sớm (e.g systemd và udev) để chứa các file tempory runtime như các file PID.
- `/mnt`: dùng để mount external filesystem. (e.g NFS)
- `/media`: dùng để mount cdrom.