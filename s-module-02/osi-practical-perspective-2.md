# Khái niệm

>_Nội dung section này được lấy chủ yếu từ video: **[OSI Model: A Practical Perspective - Part 2 - Networking Fundamentals - Lesson 2](https://www.youtube.com/watch?v=0aGqGKrRE0g&list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi&index=4)**_

## Layer 4 - Transport

- Mục tiêu cuối cùng của Layer 4 là truyền tải **Server to Service**.
- Khi một người dùng sử dụng máy tính, họ có thể vừa duyệt web, vừa nghe nhạc, vừa chat, ... Vậy làm thế nào để các gói tin có thể được truyền tải đến đúng các phần mềm trên máy người dùng?
- MAC và IP chỉ **đảm bảo gói tin được truyền đến host**, không đảm bảo được gói tin được truyền đến ứng dụng nào trên host.
- Layer 4 sẽ "lọc các data đầu vào" và cho phép các data này truyền tải đến đúng chương trình trên host.

  ![img](/images/sub-module-2/gif-21.gif)

- Giống như việc Layer 2 cần thông tin về MAC để thực hiện Hop to Hop, Layer 3 cần IP để thực hiện End to End, thì Layer 4 sẽ cần Port để thực hiện Service to Service.
  - Có hai tập port: 0-65535 cho TCP và 0-65535 cho UDP.
  - TCP và UDP là **hai chiến lược khác nhau** dùng để **phân biệt luồng data**.
  - TCP **ưu tiên độ tin cậy** còn UDP **ưu tiên hiệu quả truyền tải**.
- Giống như các layer khác, các gói tin khi truyền tải cũng sẽ thêm một **L4 Information delivery** chứa thông tin về port để cho phép gói tin được truyền tải đúng đến chương trình trong host.

  ![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2023-09-48.png) 

- Ví dụ: 
  - Một người dùng sử dụng máy tính cá nhân `1.1.1.1` để kết nối đến 3 server lần lượt là `www.bank.com - 2.2.2.2:443`, `wwww.site.com - 3.3.3.3:80` và `chat server - 4.4.4.4:6667`.
  - Người dùng muốn kết nối đến `wwww.site.com`, cho nên họ gửi một request đến `3.3.3.3:80`, chú ý: trước khi thiết lập kết nối, client **chọn một port ngẫu nhiên** đang trống trên máy để kết nối đến server _(Điều này được thực hiện qua một cơ chế gọi là **Dynamic PAT**, chúng ta sẽ đề cập sau)_. 
  - Sau khi chọn xong port ngẫu nhiên, cho rằng là port :9999, người dùng tiến hành đính kèm các thông tin cần thiết bao gồm: 
    - `SRC = 1.1.1.1:9999`
    - `DST = 3.3.3.3:80`
    
    ![img](/images/sub-module-2/image%20copy%202.png)

  - Khi `www.site.com` response lại yêu cầu của client, gói tin trông như sau:
    - `SRC = 3.3.3.3:80`
    - `DST = 1.1.1.1:9999`
    
    ![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2023-22-51.png)

  - Dễ dàng nhận thấy, thông tin hai gói tin về cơ bản có SRC và DST ngược lại với nhau.
  - Quá trình này cũng diễn ra tương tự nếu client gửi request đến các server khác nhau.

    ![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2023-24-12.png)

  - Ngoài ra, cơ chế này còn cho phép một client **có thể gửi nhiều request đồng thời đến server**, bởi vì lúc này đây, mỗi gói tin gửi đến cùng một server vẫn sẽ không bị overlap vì chúng có port khác nhau.

    ![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2023-26-11.png)

## Layer 5, 6, 7 - Application Layer
- Tại sao lại gộp 5, 6, 7 vào cùng một Layer? Vì vào thời gian đầu khi mà mô hình OSI được tạo ra, các Layer này có chức năng **độc lập với nhau một cách rõ ràng**. Nhưng giờ đây, sự phân biệt giữa chúng hiện đang trở nên mờ nhạt hơn, các ứng dụng hầu như có thể implement 3 layer này theo bất kì cách nào mà chúng muốn, thế nên để cho đơn giản thì thông thường, 3 layer trên cùng này thường được gọi chung là **Application Layer**.
- Thậm chí, trên thực tế, ở các mô hình mạng khác chẳng hạn như TCP Model, 3 Layer 5, 6, 7 thực sự đã bị gộp thành một Layer như sau

  ![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2023-31-59.png)

- Ở section này, chúng ta tạm thời sẽ **không** cố phân biệt 3 layer này với nhau.

## Flow in OSI Model
Sau khi đã tìm hiểu hết sơ lược về các layer trong mô hình OSI, chúng ta sẽ xem cách mà một data được truyền tải thông qua mô hình này.

1. Ta có hai máy tính cần giao tiếp với nhau, Sender đầu tiên sẽ tạo ra data cần truyền tải, sau đó data này sẽ đi qua 3 Layer Applicaton và sẽ trải qua một quá trình gọi là **Encapsulation**

  ![img](/images/sub-module-2/gif-22.gif)

2. Data được đưa xuống **Layer 4 - Transport**, và như chúng ta đã biết, Layer 4 sẽ cần thêm một thông tin về port mà data này sẽ được truyền tải, lấy ví dụ là TCP.
   
   Sau khi được gắn port, data sẽ được gọi là **segment**.

   ![img](/images/sub-module-2/gif-23.gif)

3. Segment sau đó được đưa xuống **Layer 3 - Network**, tại đây, thông tin về địa chỉ IP được thêm vào header của segment, và segment giờ được gọi là **packet**.

   Chúng ta thấy rằng, packet về bản chất vẫn chứa thông tin về port đã được gắn vào từ Layer 4, nhưng do các layer trong mô hình thực hiện các chức năng độc lập với nhau, Layer 3 đơn giản **không quan tâm đến thông tin khác** ngoài địa chỉ IP, thế nên thông tin về TCP đã bị làm mờ trong packet.

   ![img](/images/sub-module-2/gif-24.gif)

4. Packet được chuyển xuống **Layer 2 - Data Link** và được gắn thêm thông tin về địa chỉ MAC vào header, trở thành một **Frame**.
   
   Tương tự, Layer 2 cũng **không quan tâm đến thông tin khác** ngoài địa chỉ MAC, cho nên các thông tin khác bị làm mờ đi (thực chất được xem là một chuỗi bit).

   ![img](/images/sub-module-2/gif-25.gif)

5. Các frame sau khi được chuyển xuống **Layer 1 - Physical** sẽ được chuyển sang các chuỗi bit 0 và 1 và được truyền tải đi qua wire.

   ![img](/images/sub-module-2/gif-26.gif)

Cuối cùng, ở host nhận, một quá trình tương tự diễn ra nhưng **ở chiều ngược lại** được gọi là **De Encapsulation** để dịch ngược chuỗi bit thành data để host đích tiêu thụ.

