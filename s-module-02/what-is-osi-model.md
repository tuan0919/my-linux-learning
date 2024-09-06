### Sơ lược

**OSI viết tắt cho Open Systems Interconnection**, trong đó open nghĩa là "không độc quyền". Là kiến trức 7 layer với mỗi layer có một chức năng riêng biệt để thực hiện. Tất cả 7 layer này sẽ phối hợp với nhau để truyền tải dữ liệu từ người gửi đến người nhận.

Mô hình OSI cung cấp một **nền tảng lí thuyết** để hiểu được cách **giao tiếp qua mạng**. Tuy nhiên, nó thường không được implement một cách trực tiếp trên các **phần cứng** hoặc **phần mềm** liên quan đến mạng trong thực tế. Thay vào đó, **một giao thức** và các **công nghệ** sẽ thường được thiết kế dựa trên các nguyên tắc được nêu trong mô hình OSI để tạo điều kiện thuận lợi cho hoạt động truyền tải dữ liệu và kế t nối mạng hiệu quả.

### Mô hình OSI là gì
Mô hình OSI, được tạo ra năm 1984 bởi ISO, là một reference framework được dùng để giải thích quá trình truyền tải dữ liệu giữa máy tính với nhau. Nó được chia ra thành **7 layer hoạt động cùng nhau** để thực hiện các **tác vụ mạng**, cho phép một cách tiếp cận có hệ thống hơn đối với mạng máy tính.

![img](/images/sub-module-2/OSI-Model.png)

### Data Flow trong mô hình OSI
Khi chúng ta truyền tải thông tin từ một thiết bị đến một thiết bị khác, nó di chuyển thông qua 7 layer của mô hình OSI. Đầu tiên dữ liệu truyền tải xuống 7 layer từ phía người gửi và sẽ được truyền tải ngược lên 7 layer từ phía người nhận.

Luồng dữ liệu được truyền tải trong mô hình OSI theo từng bước:
- **Application Layer**: Ứng dụng tạo ra data.
- **Presentation Layer**: Data được format và mã hóa.
- **Session Layer**: Kết nối được thành lập và quản lí.
- **Transport Layer**: Dữ liệu được chia nhỏ ra thành các segments để được chuyển đi.
- **Network Layer**: Các segments được đóng gói thành các packes và được định tuyến.
- **Data Link Layer**: Các packet được đóng khung (framed) và gửi đến thiết bị tiếp theo.
- **Physical Layer**: Frame được chuyển thành các bit và truyền tải đi.
Mỗi layer thêm vào một thông tin cụ thể và đảm bảo dữ liệu sẽ đến được đích đến chính xác, và các bước này sẽ được đảo ngược ở nơi đến.

![img](/images/sub-module-2/cn1.png)

### Các giao thức trong mô hình OSI
Có hai giao thức được sử dụng trong mô hình này là *giao thức hướng liên kết* và *giao thức không liên kết*.
#### Giao thức hướng liên kết (Connection Oriented)
Trước khi bắt đầu truyền dữ liệu, các thực thể trong cùng một tầng của 2 hệ thống khác nhau cần phải thiết lập một liên kết logic chung. Chúng tiến hành trao đổi, thương lượng với nhau về tập các tham số sẽ sử dụng trong quá trình truyền dữ liệu, có thể là cắt bớt hoặc hợp nhất dữ liệu, liên kết sẽ được hủy bỏ. Việc thiết lập liên kết logic này sẽ giúp nâng cao độ tin cậy và an toàn.
#### Giao thức không liên kết (Connectionless)
Với các giao thức không liên kết chỉ có giai đoạn duy nhất truyền dữ liệu và dữ liệu khi này được truyền độc lập trên cái tuyến khác nhau.
### Vai trò và chức năng của 7 layer OSI
#### Layer 7 - Application Layer
Application Layer là lớp trên cùng, xác định giao diện giữa người sử dụng và môi trường OSI. Tầng ứng dụng được sử dụng bởi phần mềm người dùng cuối như trình duyệt web và ứng dụng email. Nó cung cấp các giao thức cho phép phần mềm gửi, nhận thông tin và trình bày dữ liệu có ý nghĩa cho người dùng.

Một vài ví dụ về giao thức lớp ứng dụng là Hypertext Transfer Protocol (HTTP - Giao thức truyền siêu văn bản), Post Office Protocol (POP - Giao thức bưu điện), Simple Mail Transfer Protocol (SMTP - Giao thức truyền thư đơn giản), Domain Name System (DNS - Hệ thống tên miền) và File Transfer Protocol (FTP - Giao thức truyền tệp)

#### Layer 6 - Presentation Layer
Tầng thứ hai kế tiếp **Application layer** là **Presentation layer**, Layer này sẽ giải quyết các vấn đề liên quan đến các cú pháp và ngữ nghĩa của thông tin được truyền.

**Presentation layer** xác định cách hai thiết bị sẽ mã hóa và nén dữ liệu để nó được nhận một cách chính xác ở đầu bên kia. **Presentation layer** lấy bất kỳ dữ liệu nào được truyền bởi **Application layer** và chuẩn bị cho việc việc truyền qua Layer phiên.

Layer này chịu trách nhiệm chính trong việc chuẩn bị dữ liệu để nó có thể được sử dụng bởi **Application layer**. Nói cách khác, Layer 6 làm cho dữ liệu hiển thị cho các ứng dụng sử dụng. **Presentation layer** chịu trách nhiệm dịch, mã hóa và nén dữ liệu.

Hai thiết bị đang giao tiếp có thể sử dụng các phương pháp mã hóa khác nhau, do đó Layer 6 chịu trách nhiệm dịch dữ liệu đến thành một cú pháp mà lớp ứng dụng của thiết bị nhận có thể hiểu được. Nếu các thiết bị đang giao tiếp qua kết nối được mã hóa, Layer 6 chịu trách nhiệm thêm mã hóa ở đầu người gửi cũng như giải mã hóa ở đầu người nhận để nó có thể hiển thị **Application layer** với dữ liệu có đọc được, không được mã hóa.

Cuối cùng, **Presentation layer** cũng chịu trách nhiệm nén dữ liệu mà nó nhận được từ lớp ứng dụng trước khi phân phối đến Layer 5. Điều này cải thiện tốc độ và hiệu quả giao tiếp bằng cách giảm thiểu lượng dữ liệu sẽ được truyền tải.  