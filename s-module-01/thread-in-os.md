### Khái niệm về Thread (Luồng)
Một luồng là một dòng tuần tự bên trong một process. Các thread còn được gọi là các lightweight process vì chúng thực thi các thuộc tính khác nhau của một process. Mỗi thread chỉ thuộc về chính xác một process. Trong hệ điều hành hỗ trợ đa luồng, một process có thể bao gồm nhiều threads. Nhưng các các thread chỉ có thể được tận dụng nếu như có nhiều hơn 1 CPU nếu không thì hai threads phải thực hiện *context switch* trên một CPU đơn.

### Threads trong hệ điều hành là gì?
Bên trong một process, một threads nghĩa là dãy các activity tuần tự đang được thực hiện một cách độc lập với nhau, các activities này còn được biết đến như là một *luồng các thao tác thực thi* hay *luồng điều khiển* (thread control). Ngày nay, bất kì hệ điều hành nào cũng có thể thực thi một thread, chúng ta có thể nói, một process có thể có nhiều luồng.

### Tại sao chúng ta cần đến thread?
- Threads chạy một cách song song với nhau sẽ tăng hiệu suất của chương trình. Mỗi thread sẽ có riêng CPU state và stack, nhưng chúng chia sẻ chung địa chỉ nhớ của process cũng như môi trường của process đó.
- Threads có thể chia sẻ data với nhau nên chúng không cần dùng đến kĩ thuật như *giao tiếp inter-process*. Giống với process, các thread cũng có các trạng thái như *ready*, *executing*, *blocked*, ...
- Có thể gán độ ưu tiên lên các thread khác nhau giống như process, và thread có độ ưu tiên cao nhất sẽ được lập lịch trước tiên.
- Mỗi thread cũng có một *khối điều điển* (Thread Control Block - TCB). Giống như process, *context switch* cũng xảy ra đối với thread, và các nội dung thanh ghi cũng được lưu vào TCB. Và vì các threads chia sẻ địa chỉ nhớ và tài nguyên với nhau, cho nên *đồng bộ hóa* cũng là yêu cầu đối vớin nhiều hoạt động khác nhau khi thao tác với threads.
### Các loại threads bên trong hệ điều hành
Threads có hai loại, được mô tả bên dưới.

- Thread cấp độ người dùng.
- Thread cấp độ kernel.

![img](/images/sub-module/Threads.png)

### Khác biệt giữa Process và Thread
Điểm khác biệt chính là các thread trong cùng một process có thể chia sẻ chung một vùng nhớ, trong khi đó các process sẽ chạy trong các vùng nhớ riêng biệt. Các threads không độc lập hoàn toàn với nhau như process, và kết quả là, các thread có thể chia sẻ giữa chúng với nhau các code section, data section và tài nguyên OS. Nhưng, giống nhhư process, một thread có bộ đếm chương trình (program counter - PC), tập các thanh ghi và vùng nhớ stack của riêng nó.

### Thế nào là đa luồng? (Multi-Thread)
Một thread được ví như là một tiến trình nhẹ. Ý tưởng để đạt được được tính song song là việc chia nhỏ một process ra thành nhiều threads. Ví dụ, trong trình duyệt, nhiều tab có thể chạy ở các thread khác nhau. MS Word sử dụng nhiều threads, một thread để format text, một thread để xử lí input, vv...

Đa luồng là một kĩ thuật được sử dụng trong hệ điều hành để tăng hiệu suất và tốc độ phản hồi của máy tính. Đa luồng cho phép nhiều thread (các tiến trình nhẹ) chia sẻ cùng tài nguyên của một process, cah83ng hạn như CPU, bộ nhớ và thiết bị I/O.

![img](/images/sub-module/Screenshot-from-2024-02-26-11-48-56-768.png)

#### Lợi ích của thread đối với hệ điều hành
- **Reponsiveness**: Nếu process được chia ra thành nhiều thread, thì khi một thread hoàn thành việc thực thi của nó, thì output của nó sẽ có thể ngay lập tức được trả về.
- **Context Switch nhanh hơn**: Thời gian context switch giữa các thread thấp hơn khi so với context switch của một process.
- **Sử dụng hiệu quả hệ thống multiprocessor**: Nếu chúng ta có nhiều thread bên trong một process, thì chúng ta có thể thiết lập cho nhiều thread chạy trên nhiều processors. Điều này khiến cho quá trình thực thi nhanh hơn.
- **Chia sẻ tài nguyên**: Các tài nguyên như code, data, và các file có thể được chia sẻ giữa các thread bên trong một process. Lưu ý: Bộ nhớ stacks và các thanh ghi không thể được chia sẻ giữa các thread.
- **Giao tiếp**: Giap tiếp giữa các thread đơn giản hơn, vì các thread chia sẻ cùng một không gian địa chỉ. Trong khi đó đối với process chúng ta cần phải tuân theo một số kĩ thuật giao tiếp nhất định để có thể cho phép hai process giao tiếp được với nhau.
- **Tăng cường throughput của hệ thống**: Nếu một process được chia thành nhiều thread, và mỗi thread function được xem như là một job, thì số lượn job được hoàn thành trên mỗi một đơn vị thời gian sẽ được tăng lên, qua đó tăng lượng throughput của hệ thống.