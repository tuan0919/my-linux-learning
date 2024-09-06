### Khái niệm cơ bản về Process
Process là một chương trình trong quá trình thực thi. Ví dụ, khi chúng ta viết một chương trình bằng C hoặc C++ rổi compile nó, compiler tạo ra các mã nhị phân. Các đoạn code gốc và các đoạn code nhị phân đều là chương trình. Khi chúng ta thực sự chạy các mã nhị phân, nó trở thành một process. Một process là một thực thể "động" khác với cho một chương trình, được xem như là một thực thể "bị động". Một chương trình đơn lẻ có thể tạo ra nhiều process khi nó chạy nhiều lần; chẳng hạn, khi chúng ta mở một file .exe hoặc một file nhị phân nhiều lần, nhiều instance được tạo ra (nhiều process được tạo ra).

### Process Management là gì?
Process mangament là một phần quan trọng của hệ điều hành. Nó điều khiển cách mà một process được thực hiện, và điều khiển cách mà máy tính hoạt động bằng cách kiểm soát các process đang hoạt động. Việc này bao gồm dừng process, cài đặt process nào nên được chú ý, và nhiều hơn thế nữa. Chính chúng ta cũng có thể tự kiểm soát process trên máy tính của mình nếu muốn.

OS có nhiệm vụ điều khiển việc bắt đầu, dừng và lập lịch cho các process, hay nói cách khác là các chương trình chạy trên hệ thống. Hệ điều hành sử dụng nhiều phương pháp khác nhau để ngăn chặn deadlocks, tạo điều kiện thuận lợi cho việc giao tiếp liên process và đồng bộ hóa các process. Quản lý process một cách có hiệu quả sẽ đảm bảo phân bổ tài nguyên hợp lý, thực thi process không gặp xung đột và hiệu suất hệ thống tối ưu. Thành phần thiết yếu này của hệ điều hành cho phép thực thi nhiều ứng dụng cùng một lúc, tăng cường khả năng sử dụng và khả năng phản hồi của hệ thống.

### Process trông như thế nào trong bộ nhớ?
Một process trong bộ nhớ sẽ được chia ra thành các phần riêng biệt, và mỗi phần sẽ có một mục đích riêng biệt. Dưới đây thể hiện một process sẽ trông như thế nào trong bộ nhớ:

![img](/images/sub-module/process.png)

- **Text section**: Trong một process, Text Section (hay còn gọi là Code Segment) là phần bộ nhớ chứa mã lệnh thực thi của chương trình. Đây là nơi lưu trữ các lệnh của chương trình đã được biên dịch từ mã nguồn, sẵn sàng để CPU thực thi.
- **Data section**: là phần bộ nhớ chứa dữ liệu toàn cục và tĩnh của chương trình. Nó được phân bổ khi chương trình bắt đầu chạy và có thể bao gồm các biến và cấu trúc dữ liệu mà chương trình cần trong suốt thời gian thực thi.
- **Stack section**: là phần bộ nhớ được sử dụng để quản lý các cuộc gọi hàm và dữ liệu tạm thời trong suốt thời gian thực thi của chương trình. Đây là nơi các biến cục bộ, các tham số hàm, và thông tin cần thiết cho việc thực thi các hàm được lưu trữ.
- **Heap section**: là phần bộ nhớ được sử dụng để cấp phát bộ nhớ động, tức là bộ nhớ mà kích thước có thể thay đổi trong suốt thời gian thực thi của chương trình.

### Các đặc điểm của một Process:

Một process có thể có các thuộc tính sau đây:

- **Process Identifier (PID)**: là *mã định danh* được hệ điều hành gán cho để phân biệt giữa các process khác nhau.
- **Process state**: là *trạng thái* của process, có thể có các trạng thái như: *New*, *Ready*, *Running*, *Waiting* hoặc *Terminated*.
- **CPU Registers**: giúp lưu trữ và quản lý các trạng thái hiện tại của process, bao gồm địa chỉ lệnh, dữ liệu tạm thời, và thông tin điều khiển. (các thanh ghi này cần phải được lưu trữ và phục hồi khi mà process được swap ra và swap vào CPU).
- **Các thông tin tính toán**: Lượng CPU được sử dụng cho việc thực hi process, thời gian giới hạn, Id thực thi, vv...
- **Các thông tin về tình trạng I/O**: thông tin về các thiết bị được cấp phát cho process, các file đã mở, vv...
- **Các thông tin lập lịch CPU**: chẳng hạn như độ ưu tiên (mỗi process sẽ có một độ ưu tiên nhất định, chẳng hạn một process ngắn hơn được gán độ ưu tiên cao hơn trong bộ lập lịch *shortest job first*).

Tất cả các thuộc tính trên của một process còn được biết đến là **ngữ cảnh của process** hay **process context**. Mỗi process có một proces control block (PCB) của riêng nó, hay nói cách khác mỗi process sẽ có một PCB độc nhất và tất cả các thuộc tính phía trên là một phần của PCB.

### Các trạng thái (state) của một process
Một process có thể có một trong các trạng thái dưới đây:
- **New**: Process vừa mới tạo hoặc process đang được tạo - tạo ra process.
- **Ready**: Sau khi tạo xong, process được chuyển vào trạng thái Ready, tức là process sẵn sàng để thực thi.
- **Wait (hoặc block)**: Khi một process yêu cầu một tác vụ I/O.
- **Complete (hoặc Terminated)**: Khi một process hoàn thành việc thực thi của nó.
- **Suspended Ready**: khi mà hàng đợi READY bị full, một số process sẽ chuyển sang suspend ready.
- **Suspended Block**: Khi mà hàng đợi WAITING bị full.

![img](/images/sub-module/process-states1.png)

### Process Operations
*Process operation bên trong hệ điều hành* đề cập đến các activities khác nhau mà hệ điều hành thực hiện để quản lí các process. Những operation này bao gồm *khởi tạo process*, *lập lịch process*, *thực thi process* và *kill process*. Dưới đây là một số process operation trọng yếu:

![img](/images/sub-module/Screenshot-2024-07-09-113355.png) 

#### Khởi tạo process
Quá trình khởi tạo một process trong OS là các hành động tạo ra một process mới. Process mới này là một thể hiện của một chương trình và có thể thực thi một cách độc lập.

#### Lập lịch process
Một khi process sẵn sàng để chạy, nó được đặt vào "READY queue". Nhiệm vụ của bộ lập lịch là chọn một process từ queue này và bắt đầu thực thi nó.

#### Thực thi process
Thực thi nghĩa là CPU bắt đầu hoạt động trên process. Trong quá trình này, một process có thể: 
- Di chuyển đến một waiting queue nếu nó cần thực hiện một tác vụ I/O.
- Bị chặn nếu như có một process có độ ưu tiên cao hơn cần đến CPU.

#### Kill process
Sau khi một process hoàn thành task của nó, hệ điều hành kết thúc nó và xóa PCB của nó.

### Chuyển đổi ngữ cảnh một Process
Quá trình lưu lại ngữ cảnh (context) của một process và load context của một process khác được gọi là *Context Switching*. Theo một cách định nghĩa dễ hiểu, thì nó giống như là load và unload một process từ trạng thái *running* sang trạng thái *ready*.

#### Khi nào Context Switch xảy ra?
Context Switch xảy ra khi:

- Một process có độ ưu tiên cao hơn chuyển sang trạng thái *ready* (có độ ưu tiên cao hơn so với process đang chạy).
- Một *Interrupt* xảy ra.
- Chuyển đổi chế độ người dùng và user (mặc dù không cần thiết).
- *Preemptive CPU scheduling* được sử dụng.

#### Contedxt Switch và Mode Switch
Một switch xảy ra khi mức đặc quyền CPU bị thay đổi, ví dụ là một system call được thực hiện hoặc một lỗi xảy ra. Kernel hoạt động ở mức độ có đặc quyền cao hơn so với các task cơ bản của người dùng. Nếu một process người dùng muốn truy cập vào những thứ mà chỉ có thể được phép truy cập bằng kernel, *mode switch* phải diễn ra. Process đang được thực thi hiện tại không nên bị thay đổi trong quá trình xảy ra mode switch. Một *mode switch* thường xảy ra khi *context switch* của process xảy ra. Chỉ *kernel* mới được phép tạo *context switch*.

#### CPU-Bound và I/O Bound process
Một CPU-bound process yêu cầu nhiều thời gian CPU hơn và dành nhiều thời gian hơn ở *running state*. Một I/O-bound process yêu cầu nhiều thời gian I/O và ít thời gian CPU hơn. Một I/O-bound process dành nhiều thời gian hơn ở *waiting state*.

*Lập kế hoạch cho process* là một phần hông thể thiếu cho việc *quản lí process* của một hệ điều hành. Nó đề cập đến các cơ chế sẽ được sử dụng bởi hđh để xác định xem process nào sẽ được chạy tiếp theo. Mục tiêu của lập lịch process là cải thiện hiệu suất tổng quát của hệ thống bằng cách tối ưu hóa sử dụng CPU, tối thiểu hóa thời gian thực thi và tăng cường tốc độ phản hồi của hệ thống.

#### Các thuật toán lập lịch process
Hệ điều hành có thể sử dụng nhiều thuật toán lập lịch khác nhau để lập lịch cho process. Dưới đây là một số thuật toán phổ biến được sử dụng:
- **First-Come, First-Served (FCFS)**: Đây là thuật toán lập lịch đơn giản nhất, khi mà process sẽ được thực thi trên quy tắc "đến trước, phục vụ trước". FSFS là một thuật toán non-preemptive, tức là một khi một process bắt đầu thực thi, nó sẽ tiếp tục thực thi cho đến khi nó hoàn thành hoặc chờ đợi một I/O.
- **Shortest Job First (SJF)**: SJF là một thuật toán lập lịch chủ động chọn process có *burst time* ngắn nhất.
- **Round Robin (RR)**: Là một thuật toán lập lịch chủ động dành một khoảng thời gian cố định trong một vòng cho mỗi process. Nếu process không hoàn thành quá trình thực thi của trong khoản thời gian cụ thể, nó sẽ bị blocked và được thêm vào cuối hàng đợi. RR đảm bảo sự phân phối đều đặn trong thời gian CPU tới mọi process và tránh tình trạng starvation (*là tình trạng mà process không tiếp cận được tài nguyên nó cần để hoàn thành công việc của mình, khiến process mất rất nhiều thời gian để hoàn thành hoặc tệ hơn là không bao giờ hoàn thành*).
- **Priority Scheduling**: Thuật toán lập lịch này gán một độ ưu tiên nhất định cho mỗi process và proces nào có độ ưu tiên cao nhất sẽ được thực thi đầu tiên. Độ ưu tiên có thể được set dựa vào *process type*, *độ quan trọng*, hoặc *tài nguyên yêu cầu*.
- **Multilevel Queue**: Thuật toán lập lịch này chia hàng đợi READY ra thành nhiều hàng đợi khác nhau, và mỗi hàng đợi sẽ có một độ ưu tiên khác nhau. Process được xếp vào hàng đợi dựa vào độ ưu tiên của chúng, và mỗi hàng đợi lại sử dụng một thuật toán lập lịch riêng. Thuật toán này phổ biến trong trường hợp mà chúng ta có nhiều loại process và có nhiều mức độ ưu tiên khác nhau.

### Ưu điểm của quản lí process
- **Chạy nhiều chương trình**: Quản lí process cho phép chúng ta chạy nhiều chương trình tại một thời điểm, ví dụ, nghe nhạc trong khi đang lướt web.
- **Cách ly process**: Đảm bảo rằng các chương trình khác nhau sẽ không ảnh hưởng đến nhau, và như thế một lỗi xảy ra tại một chương trình sẽ không crash chương trình khác.
- **Sử dụng tài nguyên hợp lí**: Khiến cho các tài nguyên như thời gian CPU và bộ nhớ được chia sẻ một cách hợp lí giữa các chương trình, nên kể cả các chương trình có độ ưu tiên thấp hơn cũng có cơ hội được chạy.
- **Chuyển đổi mượt mà**: Xử lí việc chuyển đổi giữa các chương trình một cách có hiệu quả, save và load trạng thái của chúng một cách nhanh chóng để tối thiểu hóa độ trễ trong thời gian phản hồi của hệ thống.

### Nhược điểm của quản lí process
- **Overhead**: Quản lí process cũng sẽ sử dụng các tài nguyên hệ thống bởi vì OS cần duy trì các cấu trúc dữ liệu và hàng đợi lập lịch. Việc này yêu cầu đến thời gian CPU và bộ nhớ, một phần nào đó ảnh hưởng đến hiệu suất hệ thống.
- **Phức tạp**: Thiết kế và bảo trì một OS là một việc rất phức tạp bởi vì các yêu cầu về các thuật toán lập lịch và phân bổ tài nguyên.
- **Deadlocks**: Để giữ cho process chạy mượt mà cùng với nhau, OS sử dụng các cơ chế như semaphore và mutex locks. Tuy nhiên các cách trên có thể dẫn đến deadlocks, khi mà một process bị kẹt do phải chờ đợi lẫn nhau mãi mãi.
- **Làm tăng thêm quá trình context switch**: Trong các hệ thống đa nhiệm, OS thường xuyên chuyển đổi giữa các process. Lưu trữ và load các state của mỗi process (trong *context switching*) là một quá trình tốn thời gian và cần tính toán, làm chậm hệ thống. 