## Đề bài:

![img](/images/qtm/image%20copy.png)

## Bài làm

### VM_Server

- Thêm card mạng mới cho máy ảo **VM_Server**

  ![img](/images/qtm/image.png)

- Khởi động lại máy
- Gõ lệnh `systemctl restart network` để restart network service.
- Gõ `ip link show` để xem các card mạng đang có trên máy. Trong trường hợp này đang có hai card là `enp0s3` và `enp0s8`

  ![img](/images/qtm/image%20copy%202.png)

- Vào `/etc/sysconfig/network-scripts` kiểm tra thấy card `enp0s8` đang không có file script, do đó không thể kích hoạt card mạng này bằng lệnh `ifup enp0s8`
  
  ![img](/images/qtm/image%20copy%203.png)

  > _Chú ý khi một địa chỉ IP nào đó cho các card mạng này, vì chế độ kết nối đang sử dụng là **bridge**, cho nên nếu mạng hiện tại của máy thật là mạng lớp C, thường có gateway là `192.168.1.1`, thì việc set địa chỉ IP `192.168.1.1` cho card mạng sẽ dẫn đến xung đột IP._

- Set một địa chỉ IP nào đó (chẳng hạn 192.168.1.25) cho `enp0s3` bằng lệnh `vi /etc/sysconfig/network-scripts/ifcfg-enp0s3`
  
   ```
   BOOTPROTO=static
   GATEWAY0=192.168.1.1
   IPADDR0=192.168.1.25
   NETMASK0=255.255.255.0
   DEVICE=enp0s3
   TYPE=Ethernet
   ```

- Tiếp theo set một địa chỉ IP nào đó cho enp0s8, vì enp0s8 mặc định sẽ không có file nên chúng ta cần tự viết, lệnh tương tự như trên: `vi /etc/sysconfig/network-scripts/ifcfg-enp0s8`

> Nếu mạng máy tính thật đang là mạng lớp C và default gateway của máy thật là **192.168.1.1** thì không cần phải set GATEWAY làm gì cho card mạng này vì nó đang khác lớp (**192.168.2.0** và **192.168.1.0**). Để cho phép mạng lớp **192.168.2.0** được phép sử dụng gateway **192.168.1.1** thì cần thực hiện **NAT** packet từ 192.168.2.0 đi ra ngoài.

  ```
   BOOTPROTO=static
   IPADDR0=192.168.2.25
   NETMASK0=255.255.255.0
   DEVICE=enp0s8
   TYPE=Ethernet
  ```

- Kiểm tra:
  
  ![img](/images/qtm/image%20copy%205.png)


### VM1
- Cài đặt địa chỉ IP `192.168.1.10/24` cho giao diện mạng `enp0s3` bằng lệnh `vi /etc/sysconfig/network-scripts/ifcfg-enp0s3`, file cấu hình như sau:

  ```sh
  BOOTPROTO=static
  GATEWAY0=192.168.1.25
  IPADDR0=192.168.1.10
  NETMASK0=255.255.255.0
  DEVICE=enp0s3
  TYPE=Ethernet
  ```

### VM2
- Cách cài đặt tương tự VM1, nhưng mà là địa chỉ `192.168.2.10/24` (Khác mạng local). 

  ```sh
  BOOTPROTO=static
  IPADDR0=192.168.2.10
  NETMASK0=255.255.255.0
  GATEWAY0=192.168.2.25
  DEVICE=enp0s3
  TYPE=Ethernet
  ```

### Kiểm tra
Với các cấu hình hiện tại, mạng `192.168.1.0` có thể giao tiếp với mạng `192.168.2.0` thông qua VM_Server với hai gateway là `192.168.1.25` và `192.168.2.25`

![img](/images/qtm/image%20copy%206.png)

![img](/images/qtm/image%20copy%207.png)