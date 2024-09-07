# Khái niệm

>_Nội dung section này được lấy chủ yếu từ video: **[OSI Model: A Practical Perspective - Networking Fundamentals - Lesson 2a](https://youtu.be/LkolbURrtTs?list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi&t=29)**_

## Mở đầu

Mục tiêu cuối cùng của mạng là cho phép hai host có thể trao đổi data với nhau, khi cần trao đổi data mà không có mạng, chúng ta phải sao lưu dữ liệu cần trao đổi giữa máy A vào một portable media như USB sau đó gắn vào máy B và truyền tải, về cơ bản, mạng giúp chúng ta tự động hóa quá trình trên bằng cách cho phép chúng ta truyền tải dữ liệu một cách tự động qua một kết nối.

Để làm được điều này, các host trong mạng phải tuân theo một số rule nhất định. Các rule này của mạng được chia ra làm 7 layer và có tên là **OSI Model**.

Mỗi layer trong mô hình OSI sẽ thực hiện một vai trò nhất định. Nếu tất cả các layer thực hiện được và đúng vai trò của chúng, thì trao đổi qua mạng có thể được thực hiện.

Mục tiêu của section này không phải để nhớ **lí thuyết của OSI Model**, mà là có cái nhìn khái quát về  **mục đích của từng layer và cách mà nó cống hiến vào toàn bộ mô hình**.

## Layer 1 - Physical
- Dữ liệu trong máy tính tồn tại ở dạng Bit 0 và 1.
- Việc truyền tải dữ liệu giữa hai máy tính về cơ bản là bằng cách nào đó truyền tải các chuỗi bit này.
- Mục tiêu của Physical Layer là truyền tải bit.
- Nghĩa là, bất cứ thứ gì đóng góp vào việc truyền tải các số bit 0 và 1 từ máy này sang máy khác thì có thể xem là công nghệ thuộc về Layer 1.

  Chẳng hạn các loại Wire nối trực tiếp có thể được xem là thuộc về Layer 1.

  ![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2009-53-51.png)

  Kể cả wifi cũng được xem là **L1 Technologies**. (đừng quá để tâm đến chữ Physical trong tên layer).

  ![img](/images/sub-module-2/image%20copy.png)

  Ngoài ra, các Network device như **Repeater**, **Hub** cũng được xem là **L1 Technology**, vì chúng có vai trò tái tạo và truyền tải các signal, và về cơ bản chúng là một dạng mở rộng của các Wire phía trên.

## Layer 2 - Data Link
- Tương tác với các Wire (tức là Physical Layer), sẽ đặt bit vào một wire và nhận bit từ một wire.
- Các thiết bị mà Wire sẽ dùng để kết nối đến máy tính được xem là thuộc về Layer 2
  - **NIC - Network Interface Card** / **Wifi Access Card** được xem là **L2 Technologies** vì **NIC** là thành phần mà một Wire sẽ dùng để kết nối trực tiếp đến máy tính, và **Wifi Access Card** là thành phần mà sẽ kết nối đến sóng radio do wifi phát ra.
- Vai trò của Layer 2 là cho phép dữ liệu đuợc truyền tải *Hop to Hop*. Nghĩa là Layer 2 cho phép các bit 0 và 1 được truyền tải từ NIC này đến NIC khác. 
- Để đạt được mục tiêu trên, Layer 2 sử dụng một địa chỉ gọi là **địa chỉ MAC**, địa chỉ MAC là các địa chỉ có 48 bit được biểu diễn dưới dạng một chuỗi hex 12 số.
  - Ví dụ: **94-65-9C-3B-8A-E5** / **94:65:9C:3B:8A:E5** / **9465.9C3B.8AE5**.
- Mỗi máy tính có một địa chỉ MAC độc nhất.
- Ngoài ra, các **Switch** cũng được xem là **L2 Technologies**, bởi vì Switch giúp cho các máy tính có thể kết nối với nhau trong mạng, nghĩa là nếu **hai host kết nối với nhau qua Switch**, thì Switch đóng góp vào việc **giúp traffic được truyền tải** từ NIC này sang NIC kia.
- Thông thường, giao tiếp giữa các host với nhau sẽ yêu cầu nhiều hop (bước nhảy) do các host thường ở rất xa với nhau. 
    
    Vì thế chúng ta **cần nhảy** qua nhiều Router khác nhau để đến đích, mỗi Router sẽ được kết nối với một Wire cũng sẽ cần một NIC, và mỗi NIC này cũng có địa chỉ MAC của riêng chúng
  
  ![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2010-23-55.png)

- Như đã nói, Layer 2 sẽ truyền tải từ NIC này sang NIC kia (từ địa chỉ MAC này sang địa chỉ MAC kia), nghĩa là để đến được host đích, data cần *nhảy* qua nhiều MAC khác nhau.

  ![img](/images/sub-module-2/gif-12.gif)

- Thế nhưng, nếu **Layer 2** chịu trách nhiệm truyền tải data Hop to Hop như thế này, thì thứ gì sẽ đảm bảo cho data truyền được data từ **host nguồn** đến **host đích**? Đó là vai trò của **Layer 3**.

## Layer 3 - Network
- Vai trò của Layer 3 cho phép dữ liệu được truyền tải *End to End*, nghĩa là từ nguồn cho đến đích. 
- Để đạt được việc này, Layer 3 sử dụng **địa chỉ IP**. Mỗi host sẽ được gán một địa chỉ IP để xác định và IP là thứ sẽ đảm bảo dữ liệu từ host này sẽ được chuyển chính xác đến host kia.
- **L3 Technologies**: Routers, Host (hoặc bất kì thứ gì khác có địa chỉ IP đều có thể được xem là thuộc về L3).
- Chúng ta có thể tự hỏi *"nếu đã có địa chỉ MAC rồi thì tại sao lại cần thêm địa chỉ IP và ngược lại ?"*, trả lời được câu hỏi này sẽ giúp hé lộ cách mà các packet được truyền tải qua mạng.
- Lí do mà chúng ta cần đến hai loại địa chỉ là vì mỗi loại trong chúng sẽ phục vụ một mục đích khác nhau:
  - Địa chỉ IP - truyền tải End to End
  - Địa chỉ MAC - truyền tải Hop to Hop
- Ví dụ như sau: Giả sử một host cần gửi data đến host đích (hai host ở xa nhau nên cần kết nối thông qua nhiều router), data về bản chất là **một khối bit 0 và 1** và Router sẽ **không quan tâm dữ liệu bên trong** khối này.

  ![img](/images/sub-module-2/gif-13.gif)
  
  Và bởi vì, máy `10.1.1.11` biết dữ liệu cần truyền tải đến host đích là `10.8.8.88`, nó sẽ **thêm L3 delivery information** vào gói data, bao gồm địa chỉ của nó và địa chỉ của máy đích. Dữ liệu này sẽ là thông tin để thực hiện **truyền tải End to End**.

  ![img](/images/sub-module-2/gif-14.gif)

  Máy `10.1.1.11` biết được rằng, để truyền tải dữ liệu này đến máy đích, nó **cần phải đi qua Router**, cho nên nó sẽ **thêm L2 delivery information** là địa chỉ MAC của máy hiện tại và của Router đích vào trong gói tin.

  ![img](/images/sub-module-2/gif-16.gif) 

  Với hai thông tin này, gói tin được chuyển từ máy `10.1.1.11` đến Router tiếp theo, sau đó **L2 delivery information** bị xóa đi, bởi vì nhiệm vụ của nó đã hoàn thành (*L2 chịu trách nhiệm truyền tải Hop to Hop*)

  ![img](/images/sub-module-2/gif-17.gif)

  Và tương tự, sau khi gói tin đã qua Router 1, thì Router 1 biết rằng, gói tin **cần phải chuyển tiếp** sang Router 2, thế nên tương tự như cách mà host trước đó làm, nó sẽ thêm **L2 delivery information** chứa địa chỉ MAC của nó và của Router 2 vào trong gói tin và chuyển đi. Khi gói tin đến Router 2 thì cũng sẽ bị xóa **L2 delivery information** vì không cần thiết nữa.

  ![img](/images/sub-module-2/gif-18.gif)

  Tương tự vậy cho đến khi gói tin đến được Router cuối cùng, tại đây các bước trên vẫn được lặp lại, chỉ là giờ đây, địa chỉ MAC không còn là của Router nữa mà là của host đích.

  ![img](/images/sub-module-2/gif-19.gif)

  Và tại đây, **L3 delivery information** cũng **có thể được xóa đi** bởi vì nó đã hoàn thành mục đích là **chuyển data từ host gốc đến host đích**, sau đó host `10.8.8.88` có thể tiếp hành tiêu thụ gói tin này.

  ![img](/images/sub-module-2/gif-20.gif)

- Qua ví dụ trên, chúng ta thấy rằng *Layer 2* và *Layer 3* **thực hiện các chức năng khác nhau** (truyền tải Hop to Hop và End to End). Chúng ta đã nói rằng IP và MAC thực hiện hai chức năng khác nhau, và cơ bản, chúng là như vậy. 
- Thế nhưng cần lưu ý rằng, **có một protocol sẽ kết nối L2 và L3** với nhau, gọi là **ARP - Address Resolution Protocol**. Chúng ta sẽ đề cập đến giao thức này sau.

  ![img](/images/sub-module-2/Screenshot%20from%202024-09-07%2011-11-33.png)

Ở section tiếp theo, chúng ta sẽ xem xét **L4 - Transport**.