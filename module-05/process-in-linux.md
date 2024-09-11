  ## Process trong Linux là gì?

  ### Định nghĩa sơ lược
  Một *process* có thể được hiểu là một chưong trình đang hoạt động. Nó là tập hợp các components khác nhau, bao gồm data nhận được từ file, input của người dùng, các lệnh của chương trình, vv... Trong Linux, một *process* được tạo ra khi mà một ứng dụng được khởi động, một chương trình chạy, hoặc là một dòng lệnh được thực hiện. Mỗi chương trình hoặc lệnh trong Linux chỉ tạo ra một process, nhưng một ứng dụng mặt khác lại có thể tạo ra nhiều process khác nhau để đáp ứng các task khác nhau. Trong hệ thống Linux, các process thường được tạo ra bằng cách fork ra từ một process đang tồn tại khác, hay còn được gọi là parent process.

  ### Các loại process trong Linux
  Có nhiều loại process trong Linux:
  
  #### 1. Parent và Child Process
  Một *child process* là một Linux process được tạo ra bởi một process khác được biết đến như **parent process**. Một child process có thể được tạo bằng hai cách. Cách đầu tiên là sử dụng **fork system call**, thường được sử dụng trong các hệ điều hành họ **Unix**, cách còn lại là spawn method, thường được dùng hơn trong các hệ điều hành **NT Kernel** như Microsoft Windows. Một process được xem là một parent process nếu nó tạo ra một hoặc nhiều child process (subprocess).

  #### 2. Zombie và Orphan Process
  Một **zombie process** là một Linux process đã kết thúc quá trình thực hiện của nó nhưng vẫn còn entry trong process table. Zombie process thườn được tạo ra khi mà child process thực hiện xong nhưng parent process vẫn chưa đọc được exit status của nó.

  Một **orphan process** là một process sẽ tiếp tục chạy kể cả khi process cha đã hoàn thành hoặc bị terminate. Một orphan process có thể là vô tình hoặc cố ý tạo ra.

  #### 3. Daemon process
  **Daemon process** là các process dưới nền liên quan đến hệ thống. Những process này thường chạy dưới quyền root và phục vụ yêu cầu của các process khác. Daemon process thường chạy dưới nền, chờ cho một event nhất định hoặc một task cụ thể xảy ra. Daemon process, không như process thông thường, không yêu cầu một terminal điều khiển để hoạt động. Điều này có nghĩa là chúng có thể tiếp tục chạy và thực hiện nhiệm vụ của mình mà không cần phải có sự tương tác trực tiếp từ người dùng hoặc môi trường điều khiển.

  ### Các lệnh thao tác process trong Linux
  #### 1.top
  Lệnh này được sử dụng để hiển thị ra toàn bộ Linux process đang chạy trong môi trường hoạt động.

  ![img](/images/module-05/top.png)

  Lệnh top hiển thị danh sách các process đang chạy trong thời gian thực cùng với mức tiêu thụ memory và CPU của chúng. Dưới đây là phân tích output của chúng:
  - **PID**: ID được gán cho mỗi process.
  - **User**: Username của process owner.
  - **PR**: Độ ưu tiên được gán cho process trong việc lập lịch.
  - **NI**: giá trị 'nice' của một process.
  - **VIRT**: Lượng virtual memory được sử dụng bởi process.
  - **RES**: Lượng physical memory được sử dụng bởi process.
  - **S**: State của process.
  
    - 'D' = uninteruptible sleep
    - 'R' = running
    - 'S' = sleeping
    - 'T' = traced hoặc stopped
    - 'Z' = zombie
  
  - **%CPU**: Tỉ lệ tiêu thụ CPU.
  - **%MEM**: Tỉ lệ tiêu thụ RAM.
  - **TIME+**: Tổng CPU time đã được tiêu thụ bởi process.
  - **Command**: Lệnh được sử dụng để kích hoạt process.
  
  Chúng ta có thể dùng phím mũi tên lên/xuống để điều hướng lên xuống danh sách được hiển thị. Để thoát, bấm **q**. Để kill một process, highlight (chọn) process và bấm **k**.

  Một cách khác là sử dụng lệnh kill.

  #### 2. ps
  Lệnh *ps* được viết tắt cho *process status*. Hiển thị các process đang chạy, tuy nhiên không giống với lệnh top, output hiển thị không phải là realtime.

  ![img](/images/module-05/ps-command.png)

  - **PID**: Process ID.
  - **TTY**: Terminal Type.
  - **TIME**: Tổng thời gian chạy.
  - **CMD**: lệnh launch process.
  
  Để xem rõ hơn có thể sử dụng flag `-u`:

  ![image](/images/module-05//ps-u.png)

  Trong đó:
  - **%CPU**: hiệu năng tính toán mà process đang sử dụng.
  - **%MEM**: lượng bộ nhớ mà process đang chiếm dụng.
  - **STAT**: process state

  #### 3. kill
  Để dừng process, có thể sử dụng lệnh *kill*, lệnh này sẽ gửi một signal để dừng process.

  Có nhiều loại signal mà chúng ta có thể gửi. Tuy nhiên thường sử dụng nhất là 'kill -9' hay 'SIGKILL'.

  Có thể kiểm tra toàn bộ signal bằng lệnh: `kill -L`

  Signal mặc định để gửi là 15, nghĩa là **SIGTERM**. 

  Syntax của lệnh này là `kill [pid]`
  
  Cú pháp cũng hay dùng trong trường hợp không thể termninate process một cách bình thường:

  `kill -9 [pid]`

  #### 4. nice
  Dùng để thay đổi độ ưu tiên của một process. Trong Linux, chúng ta có thể cài đặt ưu tiên giữa các porocess. Giá trị ưu tiên của process được gọi là 'Niceless', Niceless có thể trong khoảng từ **-20** đến **19**. **0** là giá trị mặc định.

  Để bắt đầu một process và gán cho nó một độ ưu tiên thay cho giá trị mặc định, dùng:

  ```sh
  nice -n [value] [process_name]
  ```

  Để thay đổi giá trị nice của một process đang chạy:
  
  ```sh
  renice [value] -p 'PID'
  ```