## Lệnh ip hay dùng

ip commands là lệnh rất hay được dùng để thao tác với các tác vụ liên quan đến layer 3 (Transport), lệnh này tương đối mới và hiện đang là giải pháp thay thế cho nhiều lệnh khác cũ hơn.

- List địa chỉ ip: 
  
  `ip addr show`
- Thêm một địa chỉ ip khác vào interface: 
  
  `ip addr add <ip_address>/<subnet_mask> dev <interface>`

- Bật/ tắt một interface

  `ip link set <interface> down/up`

- Xóa địa chỉ ip ra khỏi interface:

  `ip addr del <ip_address>/<subnet_mask> dev <interface>`
- Kiểm tra routing table:

  `ip route show`
- Lấy thông tin chi tiết về route mà os sẽ dùng để kết nối đến một host nào đó:
  
  `ip route get <destination>`
- Thêm một route vào route table:
  
  `ip route add <destination> via <gateway> dev <interface>`

  **Lưu ý**: Có một chút kì lạ khi mà bình thường route table sẽ được tự động cập nhật bởi hđh thay vì chúng ta, vậy **tại sao lại cần biết lệnh này**?
  - Ví dụ chúng ta có một mạng được set up như sau:
  
  ![img](/images/module-07/Screenshot%20from%202024-09-11%2018-14-33.png)

  - Với trường hợp này, chúng ta có một mạng lớn lớp C có dải IP 192.168.1.x và một mạng nhỏ được tạo ra bởi Router 192.168.1.5
  - Giả sử máy 192.168.1.2 cần kết nối với 1 trong 3 bên phải.
  - Máy 192.168.1.2 sẽ không kết nối được vì 3 máy bên phải nằm trong mạng LAN do Router 192.168.1.5 tạo ra.
  - Thế nên, khi máy 192.168.1.2 gửi gói tin, gói tin sẽ được gửi lên router tổng, router tổng sẽ chỉ đơn giản drop gói tin này đi vì không tìm thấy bất kì thiết bị nào nằm trong mạng của nó.
  - Trong trường hợp trên, chúng ta cần **thêm route thủ công** vào routing table vì router không có khả năng biết được bên trong nó có thêm một mạng nhỏ hơn.
  - Cụ thể, chúng ta cần thêm một route mà đối với tất cả các gói tin gửi đến host có dải IP 192.168.2.x thì chúng ta sẽ dùng gateway là router 192.168.1.5
  - Lệnh tương ứng:
  
    ```
    ip route add 192.168.2.0/24 via 192.168.1.5 dev <interface>
    ````