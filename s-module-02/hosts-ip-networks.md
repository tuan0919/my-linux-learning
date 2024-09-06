# Khái niệm

>_Nội dung section này được lấy chủ yếu từ video: **[Network Devices - Hosts, IP Addresses, Networks - Networking Fundamentals - Lesson 1a](https://www.youtube.com/watch?v=bj-Yfakjllc&list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi&index=1)**_

## Hosts

**Host** là bất kỳ thíết bị nào có thể **gửi** hoặc **nhận** traffic.

![img](/images/sub-module-2/image.png)

- Các thiết bị Internet of Things (IoT) cũng có thể được xem là một host:
  - Smart TV mà bạn stream đến.
  - Các Speaker được synchronize với nhau.
  - Đồng hồ thông minh.
  - Tủ lạnh thông minh.
- Bất kì thứ gì mà gửi hoặc nhận traffic thông qua network.

Host có thể được định danh bởi hai loại: **Client** hoặc **Server**. Client sẽ khởi tạo request còn Server sẽ phản hồi.

![img](/images/sub-module-2/Screenshot%20from%202024-09-06%2018-27-36.png)

Chú ý rằng, định nghĩa *Client* hoặc *Server* phụ thuộc vào một **tình huống communication** giữa hai host, nghĩa là. Trong một thời điểm nào đó, một *File server* cần gửi yêu cầu đến *Update Server* để lấy thông tin về các phiên bản phần mềm mới, thì lúc này *File Server* sẽ đóng vai trò là **Client** còn *Update Server* sẽ đóng vai trò là **Server**.

![img](/images/sub-module-2/Screenshot%20from%202024-09-06%2018-30-08.png)

Để cho rõ ràng, thì server đơn giản là **một máy tính** được cài sẵn các phần mềm để phản hồi lại request.
- Điều này có nghĩa, chúng ta có thể biến bất kì thiết bị nào thành server chỉ bằng việc cài đặt các phần mềm cần thiết cho thiết bị trở thành Web server.

## Địa chỉ IP

Một **địa chỉ IP** là định danh của một host. Chúng ta cần địa chỉ ip để gửi hoặc nhận **packets** qua mạng.

![img](/images/sub-module-2/Screenshot%20from%202024-09-06%2018-37-01.png)

Các địa chỉ IP sẽ được "đóng dấu" vào mọi thứ mà các host send cho nhau. 

![img](/images/sub-module-2/Screenshot%20from%202024-09-06%2018-41-12.png)

Lấy ví dụ khi client `72.45.128.15` gửi một request đến `www.site.com` có ip là `136.22.17.98`. **Packet màu xanh lá** chứa thông tin về trang mà client này yêu cầu, nó (packet) sẽ được "đóng dấu" hai thông tin `SRC 72.45.128.15` và `DST 136.22.17.98` chứa địa chỉ gửi (`SRC`) và địa chỉ nhận (`DST`)

![img](/images/sub-module-2/Screenshot%20from%202024-09-06%2018-43-04.png)

Ở chiều ngược lại, khi nhận packet và phản hồi, nó trả về một **Packet màu xanh dương** cho client chứa thông tin `SRC 136.22.17.98` và `DST 72.45.128.15`.

Tất cả mọi thứ dược truyền đi ở trên mạng đều sẽ có các thông tin source ip và destination ip như trên.

IP bản thân nó chỉ là một chuỗi 32 bits. Bit = 0 hoặc 1, tức là địa chỉ IP là tổ hợp của 32 số 0 và 1 này

Những gì xảy ra là, chúng ta sẽ lấy 32 bit này, group thành 4 cụm, gọi là Octet, rồi sau đó convert Octet này thành một số thập phân. Mỗi octet khi chuyển sang hệ thập phân sẽ có giá trị dao động từ 0 - 255.

Nghĩa là mỗi số trong một địa chỉ IP sẽ có giá trị từ 0 - 255.

![img](/images/sub-module-2/Screenshot%20from%202024-09-06%2018-49-09.png)

Các địa chỉ IP này sẽ được gán theo quy tắc có tính "kế thừa".

Giả sử, tất cả các địa chỉ IP được sở hữu bởi **Tập đoàn ACME** sẽ có giá trị là `10.x.x.x`. Cho rằng, tập đoàn này có 3 cơ sở khác nhau ở 3 quốc gia khác nhau: **New York**, **London** và **Tokyo**. Mỗi cơ sở này sẽ có **các địa chỉ con chiếm dụng 1 octet** của địa chỉ tập đoàn, tương ứng lần lượt: New York (`10.20.x.x`), London (`10.30.x.x`) và Tokyo (`10.40.x.x`):

![img](/images/sub-module-2/Screenshot%20from%202024-09-06%2018-56-23.png)

Hơn nữa, trong mỗi cơ sở sẽ có 3 team khác nhau, mỗi team này cũng sẽ được cấp một tập địa chỉ con (chiếm thêm 1 octet) riêng biệt. Sales (`-.-.55.x`), Engineering (`-.-.66.x`), Marketing (`-.-.77.x`)

![img](/images/sub-module-2/Screenshot%20from%202024-09-06%2019-01-46.png)

Với cách chia như vậy, chúng ta sẽ thấy được **với mỗi một địa chỉ IP** thuộc về tập đoàn ACME, sẽ có **một phần prefix của địa chỉ** thể hiện địa chỉ này thuộc về một vị trí cụ thể nào đó trong tập đoàn. Ví dụ nếu chúng ta có địa chỉ `10.30.55.127`, thì địa chỉ này là **ACME inc**, **London**, **Sales Team**.

Việc phân cấp địa chỉ theo quy tắc kế thừa thế này được gọi là *Subnetting*, nhưng trong session này, chúng ta sẽ không đi sâu vào Subnetting.

## Network
Với ví dụ trên, mỗi một host nằm trong một team nào đó sẽ tồn tại trong một "mạng".

Mạng là thứ sẽ truyền tải traffic giữa các host với nhau.

Trong form đơn giản nhất, khi chúng ta kết nối hai host với nhau, chúng ta có cũng có một mạng.

![img](/images/sub-module-2/Screenshot%20from%202024-09-06%2019-10-40.png)

Mạng về cơ bản chỉ là một nhóm các host kết nối tương tự nhau.
- Ở nhà, có lẽ chúng ta sẽ có một mạng wifi, trong mạng này chúng ta có máy tính cá nhân, máy in laptop, điện thoại... các thiết bị khác nhau này có cùng một profile kết nối là `Home Wifi`.
- Ở ngoài đường, có thể có một profile kết nối khác là `Coffee Shop` cũng cung cấp một mạng wifi dành cho khách, các khách trong cửa hàng này cũng có các thiết bị khác nhau và đều đang kết nối đến mạng.
- Vì các thiết bị có sự khác biệt về vị trí địa lí, nên chúng ở hai mạng tách biệt nhau.

![img](/images/sub-module-2/Screenshot%20from%202024-09-06%2019-17-51.png)

Mạng cũng có thể chứa một mạng khác, giả sử chúng ta có một ngôi trường ở gần nhà, và ngôi trường đó cũng có một mạng. Nhưng trường rất rộng và có nhiều lớp, nên mỗi lớp cũng được trang bị một mạng riêng để phục vụ việc giảng dạy, nói cách khác mỗi lớp bây giờ là một mạng riêng.

![img](/images/sub-module-2/Screenshot%20from%202024-09-06%2019-21-05.png)

Các mạng nằm trong một mạng khác được gọi là mạng con. 

Thực tế ngay cả với ví dụ ban đầu về tập đoàn ACME, thì các mạng được chia theo quốc gia, team khác nhau cũng được xem là mạng con của mạng lớn hơn.

![img](/images/sub-module-2/Screenshot%20from%202024-09-06%2019-23-26.png)

Ngoài ra, một mạng cũng có thể kết nối với một mạng khác, và thay vì tất cả các network này kết nối trực tiếp với nhau theo một tổ hợp nào đó (Home wifi - Shool ; School - Coffee Shop; ...) thì **tất cả các mạng** được kết nối với nhau tại một điểm trung tâm gọi là **internet**.

![img](/images/sub-module-2/Screenshot%20from%202024-09-06%2019-25-03.png)

Bên handle các kết nối này thường là Internet Service Provider hay ISP.

Phần tiếp theo, chúng ta sẽ nói về **Repeater**, **Hub**, **Bridge**, **Switch** và **Router**.