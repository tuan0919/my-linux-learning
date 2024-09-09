# Khái niệm

> Nội dung của section này được lấy chủ yếu từ bài viết **[Network Configuration Files in Linux Explained](https://www.computernetworkingnotes.com/linux-tutorials/network-configuration-files-in-linux-explained.html)**

Linux lưu trữ cấu hình mạng trong các tập tin. Để quản lí mạng trong Linux, chúng ta cần biết về những tập tin cấu hình này.

## File cấu hình Network Interface
Linux sử dụng các file cấu hình riêng biệt cho mỗi network interface để lưu trữ địa chỉ IP của chúng và các thông tin liên quan khác. Tất cả các file cấu hình mạng này nằm trong thư mục **/etc/sysconfig/network-scripts**

Để phân biệt, linux sử dụng prefix **ifcfg-** cho các file này. Chẳng hạn đối với interface tên là **eno16777736** thì file cấu hình của nó sẽ có tên là **ifcfg-eno16777736**.

![img](/images/module-07/lt53-01-listing-network-config-files.png)

Bảng dưới đấy giải thích sơ lược các tập tin được lưu trữ trong thư mục **/etc/sysconfig/network-scripts/**

|File|Mô tả|
|----|-----|
|ifcfg-lo|Lưu trữ thông tin cấu hình cho loopback device. Loopback device là một iterface network ảo. Chúng ta có thể dùng nó để test giao thức TCP/IP có sẵn trên local host.|
|ifcfg-*|Lưu trữ thông tin cấu hình của các network interface. Mỗi file chỉ chứa thông tin cấu hình liên quan đến interface mà nó đại diện (qua tên)|
|ifup-* và ifdown-*|Chứa các đoạn script dùng để enable hoặc disable các protocol có liên quan. Chẳng hạn, file script **ifup-ppp** sẽ enable giao thức **ppp**, còn file **ifdown-ppp** sẽ disable giao thức **ppp**|

Các cấu hình đuợc lưu trữ bên trong các file cấu hình của một interface sẽ áp dụng lên interface khi chúng ta khởi động hệ thống hoặc kích hoạt interface. Để xem những cấu hình này, chúng ta có thể sử dụng lệnh **cat**. Ví dụ, để xem cấu hình của interface **eno16777736**:

```bash
cat /etc/sysconfig/network-scripts/ifcfg-eno16777736
```

![img](/images/module-07/lt53-03-listing-network-config-files.png)

## Các chỉ thị cấu hình
Bảng bên dưới liệt kê các chỉ thị quan trọng và mô tả của chúng đối với các file cấu hình network interface.

Lưu ý: Cụm từ "cấu hình IP đầu tiên" đề cập đến trường hợp một thiết bị mạng có thể có nhiều cấu hình địa chỉ IP khác nhau, chẳng hạn như trên cùng một interface, nhưng với nhiều địa chỉ IP. Các hệ điều hành cho phép một interface duy nhất (như eth0, ens33, v.v.) có thể được gán nhiều địa chỉ IP.

|Chỉ thị|Mô tả|
|-------|-----|
|BOOTPROTO|Xác định xem địa chỉ IP nên được cấp phát như thế nào.|
|BRIDGE|Chỉ định tên của network bridge.|
|BROADCAST0|Địa chỉ broadcast của IP đầu tiên.|
|GATEWAY0|Địa chỉ Gateway của IP đầu tiên.|
|DEFROUTE|Chỉ định xem có dùng interface này làm default route hay không|
|DEVICE|Device name của interface|
|DNS1|Địa chỉ IP của DNS thứ 1|
|HWADDR|Địa chỉ hardware (MAC) của interface|
|IPADDR0|Chỉ định IP đầu tiên của interface này|
|IPV6INIT|Xác định xem có sử dụng IPv6 hay không|
|NAME|Tên của interface, nếu không được chỉ định cụ thể thì là tên của device|
|NETMASK0|Netmask hay subnetmask của IP đầu tiên|
|NM_CONTROLLED|Chỉ định xem Network Manager service có được phép thực hiện thay đổi cấu hình trong file này hay không|
|ONBOOT|Active hay không interface này khi boot|
|USERCTL|Chỉ định xem non-root users có quyền active interface này hay không|
|UUID|UUID của interface này|
|TYPE|Loại interface|

Bên cạnh các chỉ thị bên trên, còn có rất nhiều chỉ thị khác mà chúng ta có thể dùng trong các file cấu hình. Để xem danh sách đầy đủ, dùng lệnh:

```bash
man nm-settings
```

## File /etc/hosts
File này sẽ map hostname đến một địa IP. Sau khi map hostname với một địa chỉ IP, chúng ta có thể sử dụng hostname để truy cập vào các service tồn tại trên IP đích. 

**Lưu ý:** 
Có hai cách để map một hostname với địa chỉ IP: **DNS Server** và file **/etc/hosts**. 

DNS server cung cấp rất nhiều chức năng. Chúng có thể map hàng triệu hostname khác nhau với các địa chỉ IP khác nhau, nhưng chúng khá là phức tạp và cần khá nhiều thiết lập khác nhau. Thông thường, chúng không được sử dụng trong các mạng có phạm vi nhỏ, mà thay vào đó đối với các mạng nhỏ, chúng ta có thể sử dụng các file **/etc/hosts**. 

File **/etc/hosts** cho phép chúng ta map các hostname với địa chỉ IP trong hệ thống nội bộ. Chúng ta cần phải update file này thủ công. Mỗi dòng trong file đại diện cho một entry riêng biệt. Nó chứa địa IP trong cột đầu tiên, phiên bản đầy đủ hay offical name của hostname ở cột thứ hai, và phiên bản ngắn gọn hay alias name ở cột thứ ba.

Ví dụ:

![img](/images/module-07/lt53-06-hosts.png)

Nếu chúng ta muốn sử dụng DNS server, thì không được update file **/etc/hosts**. Hệ thống sử dụng **/etc/hosts** đầu tiên để phân giải tên miền thành địa chỉ IP. Nó chỉ gửi truy vấn DNS khi **không tìm thấy** địa chỉ được ánh xạ tương ứng trong file đó.

## File /etc/resolv.conf

