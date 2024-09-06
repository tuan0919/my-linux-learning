### Khái niệm về đồng bộ hóa process
*Đồng bộ hóa process* là thứ tự hóa việc thực hiện của nhiều process trong hệ thống nhiều process để đảm bảo rằng chúng có thể truy cập và chia sẻ tài nguyên theo cách mà chúng ta có kể kiểm soát và dự tính được. Mục tiêu của nó là giải quyết các vấn đề về *race condition* và các vấn đề đồng bộ khác sẽ xảy ra trong một hệ thống đồng thời.

Mục tiêu chính của đồng bộ hóa proecss là đảm bảo rằng nhiều process có thể truy vào một tài nguyên dùng chung mà không ảnh hưởng lẫn nhau và ngăn chặn các khả năng xảy ra dữ liệu không nhất quán do việc truy cập đồng thời. Để đạt được điều này, các kĩ thuật đồng bộ hóa khác nhau chẳng hạn như semaphore, monitor và cirtical section được sử dụng.

Trong hệ thống đa process, đồng bộ hóa là cần thiết để đảm bảo tính bền vững và tính chính trực của dữ liệu, tránh các rủi ro về deadlocks và các vấn đề đồng bộ hóa khác. Đồng bộ hóa process là một khía cạnh quan trọng trong các hệ điều hành hiện đại, và nó đóng trò chủ chốt trong việc đảm bảo hoạt động chính xác và hiệu quả trong các hệ thống đa process.

#### Nhắc khái quát lại khái niệm về Process
Một process là một chương trình đang chạy hoặc một chương trình đang thực thi. Nó bao gồm các dòng code của chương trình và tất cả các activity mà nó cần để thực hiện nhiệm vụ của nó, chẳng hạn như sử dụng CPU, bộ nhớ và các tài nguyên khác. Tưởng tượng đến process như là một nhiệm vụ mà máy tính đang thực hiện, chẳng hạn như mở trình duyệt web và xem video.

### Các loại process
Trên cơ sở đồng bộ hóa, thì process được phân nhóm vào một trong hai loại dưới đây:

- **Process độc lập**: Việc thực thi của process này sẽ không ảnh hưởng đến việc thực thi của proces khác.
- **Process phối hợp (cooprative)**: Một process có thể ảnh hưởng hoặc bị ảnh hưởng bởi một process khác đang được thực hiện bởi hện thống.

Vấn đề trong đồng bộ process phát sinh trong trường hợp các process phối hợp bởi vì tài nguyên có thể được chia sẻ trong process phối hợp.

### Race Condition là gì?
Khi có nhiều hơn một process thực thi cùng một khối mã hoặc truy cập vào cùng một vùng nhớ hay bất kì các biến dùng chung nào đó dẫn đến *khả năng* xảy ra sự sai lệch trong kết quả đầu ra hoặc trong giá trị của các biến dùng chung, khiến cho tất cả các process khác "trong cuộc đua" xem rằng output của nó là đúng (trên thực tế là sai), *khả năng* này được gọi là *race condition*. Nhiều process truy cập và xử lí đồng thời các thao tác trên cùng một khối dữ liệu, dẫn đến kết quả phụ thuộc vào thứ tự mà các process tác động.

Khi nhiều process truy cập và xử lý các thao tác trên cùng một dữ liệu đồng thời, kết quả cuối cùng phụ thuộc vào thứ tự cụ thể mà các thao tác xảy ra. Race condition là một tình huống có thể xảy ra bên trong một *critical section* (khu vực quan trọng). Điều này xảy ra khi kết quả của nhiều thread thực thi trong critical section khác nhau tùy thuộc vào thứ tự mà các thread thực hiện.

Race condition trong critical section có thể được tránh nếu critical section được coi là *một thao tác nguyên tử* (atomic instruction). Ngoài ra, việc đồng bộ hóa các thread đúng cách bằng cách sử dụng các khóa (locks) hoặc các biến nguyên tử (atomic variables) có thể ngăn chặn race condition.

### Vấn đề Critical Section
Một critical section là một đoạn code chỉ có thể được truy cập bởi một process tại một thời điểm. Critical section chứa các biến cần phải được đồng bộ hóa để duy trì tính ổn định của dữ liệu. Vậy nên *vấn đề critical section* nghĩa là đề cập đến *cách thiết kế* để cho phép nhiều *process phối hợp* có thể truy cập các tài nguyên dùng chung mà không tạo ra các dữ liệu không nhất quán.

![img](/images/sub-module/critical-section-problem.png)

Trong *entry section*, process sẽ yêu cầu được truy cập vào **Critical Section**.

Bất kì giải pháp cho vấn đề critical section cần phải thỏa ba yêu cầu sau:

- **Mutual Exclusion**: Nếu một process đang thực thi bên trong critical section, thì không một process nào khác được phép thực thi bên trong critical section.
- **Progress**: Nếu không một process nào đang thực thi bên trong critical section và các process khác đang chờ bên ngoài critical section, thì chỉ chỉ những process *đang không thực thi* remainder section của chúng mới có quyền tham gia vào với tư cách là ứng viên cho quá trình quyết định process nào được phép truy cập tiếp theo, và việc lựa chọn này không thể được trì hoãn vô thời hạn.
- **Bounded Waiting**: Cần phải có một giới hạn nhất định cho *số lần mà process được phép truy cập vào critical section* sau khi process đã yêu cầu được truy cập và trước khi yêu cầu đó được chấp thuận.

##### Giải pháp Peterson
Giải pháp Peterson là một giải pháp dựa trên các phần mềm cổ điển cho vấn đề Critical Section. Trong giải pháp này, chúng ta cần có hai biến dùng chung:

- boolean flag[i]: giá trị khởi tạo là FALSE, ban đầu không có process nào muốn truy cập *critical section*.
- int turn: là process đến lượt được phép truy cập.

![img](/images/sub-module/peterson.png)

*Giải pháp này bảo toàn được 3 điều kiện*

**Nhược điểm của giải pháp Peterson**
- **Sử dụng Busy Waiting**: (Trong giải pháp Peterson, câu lệnh code "while(flag[j] && turn == j);" là nguyên nhân gây ra điều này. Busy waiting không được ưa chuộng vì nó lãng phí các chu kỳ CPU có thể được sử dụng để thực hiện các tác vụ khác.)
- **Giới hạn chỉ cho 2 Process**: Giải pháp Peterson chỉ có thể áp dụng cho hai process. Điều này làm cho nó không linh hoạt trong các hệ thống đa process.
- **Không thể sử dụng trên kiến trúc CPU hiện đại**: Giải pháp Peterson không thể được áp dụng trên các kiến trúc CPU hiện đại do các vấn đề về hiệu suất và các tính năng phần cứng hiện đại không tương thích với giải pháp này.

#### Semaphores
Một semaphore là một cơ chế phát tín hiệu và một thread đang chờ một semaphore có thể được thread khác phát tín hiệu đến. Điều này khác với mutex vì mutex chỉ có thể được phát tín hiệu bởi thread đang gọi hàm *wait*.

Một semaphore sử dụng hai hành động nguyên tử, *wait* và *signal* cho đồng bộ hóa các process.

Một semaphore là một biến số nguyên, chỉ có thể được truy cập thông qua hai hành động *wait()* và *signal()*. Có hai loại semaphore: *Binary semaphore* và *Counting semaphore*:

- **Binary Semaphore**: Chỉ có thể là 0 hoặc 1. Chúng còn được biết đến như một khóa mutex, là một khóa được dùng trong *mutual exclusion*. Tất cả các process có thể chia sẻ cùng một mutex semaphore được khởi tạo là 1. Sau đó, mỗi process phải chờ cho đến khi khóa trở thành 0. Sau đó, có thể làm cho mutex semaphore thành 1 và bắt đầu truy cập critical section của mình. Khi mà một process hoàn thành xong, nó phải reset giá trị của mutex semaphore thành 0 và các process khác có thể được phép truy cập vào critical section.
- **Counting Semaphores**: Chúng có thể bất kì giá trị nào mà không bị giới hạn cụ thể. Chúng có thể được dùng để kiểm soát việc truy cập đến một tài nguyên nào đó mà *cho phép* một số lượng giới hạn các truy cập *đồng thời*. Bất kì process nào muốn sử dụng tài nguyên đó, nó phải kiểm tra xem giá trị còn lại của semaphore có lớn hơn 0 hay không, tức là vẫn còn lượt cho process truy cập. Sau đó, process có thể truy cập vào critical section và phải giảm giá trị của semaphore xuống 1. Sau khi process kết thúc quá trình truy cập, nó có thể rời khỏi critical section nhưng đồng thời phải tăng  giá trị của semaphore lên 1.

### Ưu điểm của đồng bộ Process:
- Đảm bảo tính nhất quán và chính trực của dữ liệu.
- Tránh được race condition.
- Ngăn ngừa các dữ liệu không nhất quán do truy cập đồng thời.
- Hỗ trợ một cách có hiệu quả việc sử dụng các *tài nguyên dùng chung*.

### Nhược điểm của đồng bộ Process:
- Tăng thêm overhead cho hệ thống.
- Có thể dẫn đến suy giảm hiệu suất.
- Tăng độ phức tạp cho hệ thống.
- Có thể gây ra deadlock nếu không được implement đúng cách.