# Khái niệm

>_Nội dung section này được lấy chủ yếu từ video: **[Hub, Bridge, Switch, Router - Network Devices - Networking Fundamentals - Lesson 1b](https://www.youtube.com/watch?v=H7-NR3Q3BeI&list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi&index=2)**_

## Repeater

Chúng ta đã biết là một mạng cũng có thể được tạo ra bằng cách cho hai máy tính kết nối trực tiếp với nhau.

Một điều cần lưu ý, **Data truyền tải qua dây** sẽ bị **tiêu hủy** dần dần dựa vào khoảng cách mà chúng truyền tải.

Nếu hai máy tính kết nối chung một phòng, thì đây không phải là vấn đề cần phải quan tâm

![img](/images/sub-module-2/gif-1.gif)

Thế nhưng, khi khoảng cách giữa hai máy tính trở nên lớn hơn, data truyền tải lúc này có thể bị tiêu biến trước khi nó đến được host đích.

![img](/images/sub-module-2/gif-2.gif)

Trong trường hợp này, chúng ta cần đến **Repeater**, nhiệm vụ của Repeater không gì khác ngoài **tái tạo lại signal**, qua đó cho phép truyền tải data đi xa hơn.

![img](/images/sub-module-2/gif-3.gif)

## Hub

Với cách tiếp cận là **kết nối trực tiếp** các host hiện tại, thì chúng ta dễ dàng nhận thấy rằng, khi thêm các host khác vào chung một mạng, chúng ta phải tiến hành kết nối chúng với nhau một cách trực tiếp, khi chúng ta thêm 3 host thì chúng ta phải kết nối 3 host, khi chúng ta thêm 4 thì chúng ta phải kết nối 4 host lại với nhau và tương tự, có thể nhận thấy cách tiếp cận này **không dễ dàng** khi chúng ta scale mạng to hơn.

![img](/images/sub-module-2/gif-4.gif)

Do thế, chúng ta cần một thiết bị làm điểm kết nối trung tâm và cho phép các host có thể trao đổi với nhau qua nó, từ đó dễ dàng mở rộng thêm số lượng host có trong mạng. Thiết bị để giải quyết cho trường hợp này là **hub**.

![img](/images/sub-module-2/Screenshot%20from%202024-09-06%2020-11-23.png)

Một hub không gì hơn, là một **Repeater nhiều port**. Port cũng sẽ **tái tạo signal** nhưng signal sẽ được chuyển qua nhiều port.

Ví dụ, chúng ta cần gửi một packet giữa hai host (màu xanh) như hình, thì khi signal đi đến Hub, Hub sẽ tái tạo, duplicate chúng lên và gửi đến **toàn bộ host khác**.

![img](/images/sub-module-2/gif-5.gif)

Dễ dàng nhận thấy, vấn đề của Hub là tất cả mọi người trong mạng đều thấy data và tất cả mọi người trong mạng đều nhận được data, kể cả các host đấy không liên quan đến communication. Điều này dẫn chúng ta đến **Bridge**.

## Bridge

Chúng ta có hai set host, interconnect với nhau thông qua Hub, **Bridge** sẽ là thành phần đứng giữa các host được kết nối với Hub, **Bridge** chỉ có hai port, một port kết nối với set Hub-connected hosts, port còn lại kết nối với một set Hub-connected hosts khác. Bridge biết được một host **nằm ở bên nào** và nhờ đó cho phép Bridge kiểm soát commucation qua Hub **chỉ diễn ra ở một bên bridge**.

![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2000-18-06.png)

Ví dụ, chúng ta có hai host màu xanh đang cần communication với nhau qua Hub. Khi chúng gửi data qua Hub, thì hub sẽ gửi data đến toàn bộ ports, chú ý là Bridge cũng nhận được một bản copy signal do Hub gửi đến. Nhưng Bridge biết rằng hai host màu xanh đang nằm bên trái của bridge, cho nên packet sẽ **không được gửi qua bên còn lại**.

![img](/images/sub-module-2/gif-6.gif)

Mặc khác, nếu hai host màu vàng bên phải cần communication với nhau thì cũng tương tự, Bridge sẽ đảm bảo chỉ các host bên phía bên phải nhận được packet.

![img](/images/sub-module-2/gif-7.gif)

Lưu ý là, Bridge **vẫn cho phép** hai host ở hai bên giao tiếp với nhau. Khi đó packet sẽ được gửi cho cả hai set host.

![img](/images/sub-module-2/gif-8.gif)

## Switch

**Switch** giống như là sự kết hợp giữa **Hub** và **Switch**:
- Switch có nhiều port nên cho phép nó đóng vai trò là một điểm interconnection.
- Switch biết được thông tin về **host nào** đang ở **port nào**. Thế nhưng khác biệt so với Bridge là Switch biết chính xác các host nằm ở port nào.
- Switch cho phép **hai host giao tiếp** với nhau và **không gửi signal đến các host không liên quan**.

![img](/images/sub-module-2/gif-9.gif)

Switch tạo điều kiện cho giao tiếp **bên trong** một mạng.
- **Mạng**: là một tập các host có kết nối giống nhau.
- Các host bên trong một network chia sẻ chung một không gian địa chỉ IP.
- Các host kết nối với nhau thông qua Switch => chúng có kết nối giống nhau nhau => chúng cùng một mạng.

![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2000-50-56.png)

Quay lại với ví dụ mạng trong trường, chúng ta có nhiều lớp học, và mỗi lớp học **có một mạng riêng**. Giả sử Classroom 2 có IP space là `172.16.20.x`, Classroom 3 có IP space là `172.16.30.x` và **hai lớp không có nhu cầu kết kết nối mạng với nhau**. Trong trường hợp này, chúng ta có thể sử dụng hai switch để tạo thành 2 mạng độc lập với nhau như sau:

![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2000-55-06.png)

Trong trường hợp, các host cần giao tiếp qua hai mạng riêng biệt với nhau, giả sử máy `.33` cần giao tiếp với máy `.66`, Switch **không thể giải quyết được** trường hợp này vì chúng đang ở **hai mạng riêng biệt**. Lúc này chúng ta cần một thiết bị khác là **Router**.

## Router

**Router** là thiết bị có vai trò tạo điều kiện **giao tiếp qua mạng**.

![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2001-02-46.png)

Với router, chúng ta có thể cho phép `.33` và `.66` và hơn thế nữa, Router còn cho phép kết nối đến các thiết bị khác bên ngoài hai mạng trên, và thậm chí là tất cả các thiết bị hiện có trên mạng toàn cầu **Internet**.

![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2001-06-31.png)

Ngoài ra router còn cung cấp điểm điều khiển traffic (như bảo mật, lọc request, chuyển hướng request, ...). Các *thiết bị Switch truyền thống* không thể thực hiện được các tác vụ này.

Cách mà router hoạt động là chúng học được **chúng đang kết nối với mạng nào**. Chẳng hạn router trên ảnh đang biết được nó đang kết nối với các mạng là `172.16.20.x`, `172.16.30.x` và `Internet`. 

Sử hiểu biết của Router về các mạng này còn được gọi là **Route**, và các route được Router lưu trữ trong một cấu trúc gọi là **Routing Table**.

**Routing Table** - tất cả các mạng mà một Router biết đến.

Ở trên có đề cập đến **Router học được chúng đang kết nối đến mạng nào**, điều này có nghĩa là **Router có IP address trong mạng mà chúng đang kết nối đến**.

Ví dụ, trong hình này, Router đang kết nối đến hai mạng `172.16.20.x` và `172.16.30.x` bởi vì nó có địa chỉ IP trong hai mạng này, cụ thể là `172.16.20.1` và `172.16.30.254`

![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2001-16-25.png)

Hai địa chỉ trên còn được gọi là **Gateway** bởi vì, dễ dàng nhận thấy, tất cả các request bên trong hai mạng này muốn đi ra ngoài đều phải **đi qua router**, mà để đi đến router thì chúng phải dùng địa chỉ **Gateway**.

![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2001-21-46.png)

Với cái nhìn rộng hơn, Router là thứ tạo ra sự kế thừa trong các mạng và toàn bộ Internet.

Lấy ví dụ, trụ sở New York của ACME inc. có 3 team khác nhau và mỗi team có một mạng riêng, mỗi mạng này sẽ kết nối đến một router, và mỗi router này sẽ lại kết nối đến một router khác.

Lúc này, giả sử một host trong một team (Sales) muốn giao tiếp đến một host trong team khác (Marketing), dữ liệu sẽ được gửi như sau:

![img](/images/sub-module-2/gif-10.gif)

Tương tự, nếu ta có thêm một mạng tương đương là trụ sở Tokyo của ACME inc. thì để hai mạng này giao tiếp được với nhau, hai router trong hai trụ sở cũng phải bằng cách nào đấy kết nối được với nhau thông qua một router lớn hơn và tương tự... các router lớn này kết hợp với nhau tạo ra các route trong Internet, nên ta có thể  coi Internet là **một tập các router**:

![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2002-09-52.png)

Lúc này, giả sử một host trong một team ở New York muốn giao tiếp với một host trong một team ở Tokyo, data được truyền tải như sau:

![img](/images/sub-module-2/gif-11.gif)

Đây là cách mà data sẽ được truyền tải qua Internet.

## Cần nhớ

- **Routers** cho phép giao tiếp **giữa các network**.
- **Switch** cho phép giao tiếp **bên trong một network**.
- **Routing** là quá trình **di chuyển data giữa các network**.
  - Nhiệm vụ chính của một Router là thực hiện Routing.
- **Switching** là quá trình **di chuyển data bên trong network**.
  - Nhiệm vụ chính của một Switch là thực hiện Switching.

Có rất nhiều Network Devices khác nhau hiện nay:
- Access Points
- Firewall 
- Layer 3 Switches
- IDS / IPS
- Load Balancer
- Proxies

Và kể cả các Devices chỉ tồn tại trong môi trường đám mây như:
- Virtual Switches
- Virtual Routers

**Tất cả các device trên đều chỉ dùng để thực hiện Routing hoặc/và Switching.**