# CÁC DẢI MẠNG TRONG VMWARE
## Mục lục
[1. Cách kết nối mạng cho các máy ảo trên phần mềm VMware Workstation ](#cach-kn)

[2. Các chế độ kết nối mạng trên VMware](#cac-cd)

## <a name = "cach-kn"></a> 1. Cách kết nối mạng cho các máy ảo trên phần mềm VMware Workstation

-  Các Vmnet là gì? Mỗi Vmnet chính là 1 bộ chia mạng ảo hay từ chuyên môn chính là Switch ảo mà Vmware Workstation tạo ra
  * Ta thường thấy Vmnet là Vmnet1 và Vmnet8 trong máy ảo. Vì mặc định khi cài xong phần mềm VMware trong phần Network của máy thật có 2 adapter mạng VMnet1 và Vmnet8.
  * Khi tạo mấy ảo có thể tạo 1 hay nhiều ca mạng,  tuy nhiên điều bắt buộc là mỗi card mạng phải được gán vào 1 Vmnet nào đó.
- Khi cài xong VMware, mặc định trong phần Network của máy thật sẽ có 2 Adapter mạng là VMware Network Adapter VMnet1 và VMware Network Adapter VMnet8. Do đó chỉ cần đặt địa chỉ IP cho 2 card mạng này của máy thật cùng dải IP với các máy ảo cũng nối vào 2 Switch ảo này, thì máy thật và máy ảo có thể kết nối với nhau qua một trong 2 card mạng này.
- Khi các máy tính cùng được nối vào 1 Switch, nếu chúng có địa chỉ IP (có thể là tĩnh – static hoặc động – DHCP) cùng dải mạng thì chúng có thể kết nối trực tiếp với nhau. Trường hợp Switch đó có nối với 1 thiết bị thực hiện chức năng DHCP thì các máy tính để IP động sẽ nhận được địa chỉ IP từ thiết bị này. Nếu không có thiết bị cấp DHCP thì các máy tính phải đặt IP tĩnh và các IP cùng dải mạng thì mới làm việc được với nhau.

## <a name = "cac-cd"></a> 2. Các chế độ kết nối mạng trên VMware
### 1. `Card Bridge`:
 - Chế độ này sẽ sử dụng card vật lý (LAN, Wifi, Bluetooth…) của máy thật để chia sẻ kết nối. Máy tính thật có thể có nhiều card mạng vật lý.
 - Mặc định VMware để Bridge ở chế độ Automatic, tức là VMware sẽ tự động chọn một trong những card mạng vật lý của máy thật để chia sẻ kết nối.
 - Do đó khi sử dụng card mạng này IP của máy ảo sẽ cùng với dải IP của máy thật.Lưu ý: Card Bridge trên máy ảo chỉ có thể giao tiếp với card mạng thật trên máy thật.
### 2. `Card NAT`:
 - Ở chế độ NAT, VMnet không chỉ còn là 1 Switch ảo mà đúng hơn nó chính là 1 Modem (router) ảo. Kết nối đến card vật lý thật ở chế độ Bridge được coi là đường WAN của Modem ảo này.
 - IP của card mạng vật lý của máy thật ở chế độ Bridge chính là IP WAN của modem ảo
 - Các máy tính ảo có card mạng ở chế độ NAT sẽ nằm trong mạng LAN của modem
 - Tương tự như bất kỳ modem (router) nào, ở chế độ NAT, VMware cũng có chức năng cấp DHCP cho các máy tính trong mạng LAN của nó
  - Giống modem nên từ máy thật hay từ một máy tính nào đó cùng dải mạng với máy tính thật sẽ không thể kết nối trực tiếp được đến máy tính trong mạng LAN ở chế độ NAT. Mà việc kết nối này sẽ thông qua IP của card mạng thật đang ở chế độ Bridge (địa chỉ WAN của modem) thông qua các port dịch vụ. Đây chính là chức năng Open port hoặc Port forwarding của bất kỳ modem nào.
  - Card NAT chỉ có thể giao tiếp với card mạng ảo VMnet8 trên máy thật.
  - Card NAT chỉ có thể giao tiếp với các card NAT trên các máy ảo khác.
  - Card NAT không thể giao tiếp với mạng vật lý mà máy tính thật đang kết nối. 
  - Tuy nhiên nhờ cơ chế NAT được tích hợp trong VMWare, máy tính ảo có thể gián tiếp liên lạc với mạng vật lý bên ngoài.

### 3. `Card Host-Only`:
 - Switch ảo không được kết nối gì với các card vật lý của máy tính thật
 - máy tính ảo sẽ không thể kết nối được đến bất kỳ thiết bị nào ngoài máy tính thật bởi tất cả các kết nối đến các thiết bị vật lý bên ngoài đều phải thông qua đến card mạng vật lý thật của máy tính thật
 - Ở chế độ Host-Only này, Vmware có lựa chọn cho phép Vmware là 1 thiết bị cấp phát DHCP cho các thiết bị kết nối vào Switch ảo. Nếu chọn chức năng này, các thiết bị nối đến Switch ảo này sẽ nhận được địa chỉ do chính VMware cấp.
