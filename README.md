# my-linux-learning
<details>
<summary>
<b>Module 1 - Understanding Linux Concepts</b>
</summary>

- <details>
  <summary>
  <b>Unix vs Linux</b>
  </summary>

  **Unix** lần đầu tiên được phát triển cho multi-user và multi-tasking vào giữa 1970. Lúc này đã có hệ điều hành nhưng chưa cho phép thực hiện multi-user và multi-tasking cho nên Unix đã được phát triển.
  
  Sau đó Linux sinh ra trong 1991 bởi Linus Torvalds

  Linux là open-source và mostly free. Nghĩa là chúng ta có thể cài đặt Linux OS trên bất kì hardware nào, có một số distribution của Linux không hẳn miễn phí như *Redhat*. Linux code bắt nguồn từ Unix thực chất là public ra cho cộng đồng. Thế nên mọi người có thể vào và thay đổi bên trong nó và tạo ra các hđh mà họ muốn.

  Unix được sử dụng chủ yếu bởi **Sun** và hệ điều hành được gọi là **Solaris**. **Sun** bây giờ đã được mua bởi **Oracle**.

  Linux được sử dụng chủ yếu bởi cộng đồng developer hoặc một số công ty như Redhat, CentOS, Debian và còn rất nhiều nữa...

  Unix hỗ trợ tương đối ít File system hơn. Trong khi đó rất nhiều File System được hỗ trợ bởi Linux.
  </details>

- <details>
  <summary>
  <b>Hard Disk</b>
  </summary>

  Một đĩa cứng là một phần của một đơn vị, thường đc gọi là "disk drive", "hard drive", hoặc "hard disk drive", lưu trữ và cung cấp khả năng truy cập tương đối nhanh vào một lượng lớn data trên một bề mặt hoặc trên tập hợp các bề mặt được tích điện từ tính. Máy tính ngày nay thường đi kèm với một đĩa cứng chứa hàng tỉ byte (gigabyte) dung lượng lưu trữ.

  Một đĩa cứng thực sự là một tập hợp các "đĩa" xếp chồng lên nhau, mỗi cái đĩa giống như một "đĩa phát nhạc", có dữ liệu được ghi lại bằng từ tính trong các vòng tròn đồng tâm hay "tracks" trên đĩa. Một "head" (một thứ gì đó giống như kim đọc dữ liệu trên đĩa phát nhạc nhưng nằm ở một vị trí tương đối cố định) sẽ ghi (write) hoặc đọc (read) các thông tin được ghi trên các track của đĩa. Hai heads, một ở mỗi bên của một đĩa sẽ đọc hoặc ghi dữ liệu khi đĩa quay. Mỗi lần đọc ghi sẽ yêu cầu định vị dữ liệu, đây là một thao tác gọi là "seek" (Dữ liệu đã có trong disk cache sẽ được định vị nhanh hơn)

  Một đơn vị hard disk/drive đi kèm với một tốc độ quay cố định, dao động từ 4500 đến 7200 rpm. Thời gian truy cập đĩa được đo bằng milliseconds. Mặc dù vị trí vật lý có thể được xác định bằng các vị trí cylinder, track, và sector, những vị trí này thực ra được ánh xạ tới một logical block address (LBA) hoạt động với phạm vi địa chỉ lớn hơn trên các đĩa cứng ngày nay.
  </details>

- <details>
  <summary>
  <b>Disk Cache</b>
  </summary>

  Disk Cache là một cơ chế giúp cải thiện thời gian dùng để đọc hoặc ghi vào một hard disk. Ngày nay, disk cache thường được đính kèm  như là một phần của hard disk. Một disk cache còn có thể là một porition cụ thể nào đó của RAM.

  Disk cache lưu giữ dữ liệu vừa được đọc, và trong một số trường hợp, là các vùng dữ liệu lân cận có khả năng được truy cập tiếp theo. Write caching đôi khi cũng được cung cấp cùng với một số disk caches.
  </details>

- <details>
  <summary>
  <b>Inside Linux</b>
  </summary>

  - <details>
    <summary>
    <b>Kernel</b>
    </summary>

    - Là lõi của hệ thống UNIX. Được load khi hệ thống khởi chạy (boot), là một chương trình điều khiển cư trú trong bộ nhớ (memory-resident control program), nghĩa là một loại phần mềm hệ thống được nạp vào bộ nhớ chính của máy tính và lưu trú tại đó để kiểm soát và quản lý tài nguyên của hệ thống máy tính, chẳng hạn như bộ nhớ, thiết bị ngoại vi và các tiến trình (processes).
    - Quản lý toàn bộ tài nguyên của hệ thống, trình bày chúng cho bạn và mọi người dùng khác như một hệ thống nhất quán. Cung cấp dịch vụ cho các ứng dụng người dùng như quản lý thiết bị, lập lịch tiến trình, v.v.
    - Một số chức năng được thực hiện bởi Kernel như:
      - Quản lí bộ nhớ của máy và cấp phát chúng cho mỗi tiến trình.
      - Lập lịch các thao tác được thực hiện bởi CPU và nhờ thế các thao tác được thực hiện một cách hiệu quả nhất.
      - Thực hiện việc chuyển dữ liệu từ một phần của máy tính sang phần khác.
      - Diễn giải và thực thi các lệnh từ shell.
      - Thực thi quyền truy cập tệp tin.
    </details>

  - <details>
    <summary>
    <b>Shell</b>
    </summary>

    - Mỗi khi chúng ta login vào hệ thống Unix, chúng ta được đặt vào một chương trình shell. Prompt của shell này thuờng được hiển thị tại vị trí con trỏ trên màn hình của chúng ta. Để hoàn thành công việc của mình, chúng ta nhập lệnh vào promt này.
    - Shell là một trình diễn giải lệnh; nó nhận từng lệnh và chuyển nó đến kernel của hệ điều hành để thực thi. Sau đó, nó hiển thị kết quả của thao tác này trên màn hình.
    - Trên bất kỳ hệ thống UNIX nào, thường có nhiều loại shell khác nhau, mỗi loại có những ưu điểm và nhược điểm riêng.
    - Các người dùng khác nhau có thể sử dụng các shell khác nhau. Ban đầu, quản trị viên hệ thống của bạn sẽ cung cấp một shell mặc định, nhưng bạn có thể thay đổi hoặc ghi đè lên nó. Các shell phổ biến nhất thường có trên hệ thống bao gồm:
      - Bourne shell (sh)
      - C shell (csh)
      - Korn shell (ksh)
      - TC shell (tcsh)
      - Bourne Again shell (bash)
    - Mỗi shell cũng bao gồm ngôn ngữ lập trình riêng của nó. Các tệp lệnh, được gọi là "shell scripts," được sử dụng để thực hiện một chuỗi các tác vụ.
    </details>

  - <details>
    <summary>
    <b>Utilities</b>
    </summary>

    - UNIX cung cấp hàng trăm chương trình tiện ích (utilities programs), thường được gọi là các lệnh (commands).
    - Các lệnh UNIX thực hiện các chức năng phổ quát, chẳng hạn như:
      - editing
      - file maintenance
      - printing
      - sorting
      - programming support
      - online info etc.
    - Tính module: các chương trình đơn lẻ có thể nhóm lại để thực hiện các tác vụ phức tạp.
    </details>
  </details>

- <details>
  <summary>
  <b>Operating system</b>
  </summary>

  Một hệ điều hành hay OS là một chương trình cho phép các phần cứng máy tính có thể tương tác và giao tiếp với các phần mềm trên máy tính. Nếu không có hệ điêu hành, các chương trình máy tính và phần mềm sẽ trở nên vô dụng.

  OS là chương trình sau khi được tải vào máy tính bởi một chương trình khởi động (boot program), sẽ quản lý tất cả các chương trình khác trong máy tính. Các chương trình khác được gọi là ứng dụng hoặc chương trình ứng dụng. Các chương trình ứng dụng sử dụng hệ điều hành bằng cách gửi yêu cầu dịch vụ thông qua một giao diện chương trình ứng dụng (API) đã được định nghĩa. Ngoài ra, người dùng có thể tương tác trực tiếp với hệ điều hành thông qua giao diện người dùng, chẳng hạn như ngôn ngữ lệnh hoặc giao diện người dùng đồ họa (GUI).

  Một hệ điều hành sẽ thực hiện các dịch vụ sau đây cho chương trình:
  - Trong một hệ điều hành đa nhiệm, nơi nhiều chương trình có thể chạy đồng thời, hệ điều hành xác định các ứng dụng nào nên chạy theo thứ tự nào và mỗi ứng dụng được phép sử dụng bao nhiêu thời gian trước khi chuyển cho ứng dụng khác.
  - Nó quản lý việc chia sẻ bộ nhớ nội bộ giữa nhiều ứng dụng.
  - Nó xử lý việc nhập và xuất dữ liệu từ và đến các thiết bị phần cứng gắn liền, chẳng hạn như ổ cứng, máy in.
  - Nó truyền message tới mỗi ứng dụng hoặc người dùng đang tương tác (hoặc đến một operator trong hệ thống) về trạng thái hoạt động và bất kì lỗi nào có thể xảy ra.
  - Nó có thể chuyển giao việc quản lý cho các **batch job** (chẳng hạn như thao tác in) và cho phép ứng dụng khởi tạo không phải chịu trách nhiệm thao tác.
  - Trong các máy tính có thể xử lí đồng thời. Một hệ điều hành có thể quản lí việc phân chia chương trình để có thể chạy trên nhiều processor tại một thời điểm.
  </details>

- <details>
  <summary>
  <b>Various Parts of an Operating System</b>
  </summary>

  UNIX và các hệ điều hành giống UNIX (như Linux) bao gồm một Kernel và một số chương trình hệ thống (system program). Ngoài ra, còn có các chương trình ứng dụng (application program) để thực thi công việc. Kernel là phần cốt lõi của hệ điều hành. Thực tế thì Kernel thường bị nhầm lẫn là hệ điều hành nhưng không phải vậy. Hệ điều hành bản thân nó cung cấp nhiều dịch vụ hơn so với Kernel.

  Nó theo dõi các tập tin trên đĩa, khởi động chương trình và chạy chúng một cách đồng thời, cấp phát bộ nhớ và các tài nguyên khác nhau cho nhiều process, nhận các packet và gửi chúng thông qua mạng và tương tự như vậy. Kernel bản thân nó thực hiện rất ít việc, nhưng nó cung cấp các công cụ mà các dịch vụ có thể được xây dựng dựa trên. Ngoài ra nó cũng ngăn chặn bất kì ai truy cập trực tiếp vào các phần cứng, ép họ sử dụng các công cụ mà nó cung cấp. Với cách này Kernel sẽ cung cấp được một số bảo vệ cho người dùng. Các công cụ được cung cấp bởi Kernel được sử dụng thông qua system call.

  Các system program sử dụng tool được cung cấp bởi Kernel để implement một số service được yêu cầu bởi hệ điều hành. System program, và tất cả các loại program khác, chạy *on top* của một Kernel, hay còn được gọi là *user mode*. Sự khác biệt giữa *system program* và *application program* nằm ở mục đích sử dụng:
  - **application program - chương trình ứng dụng**: được thiết kế để thực thi các công việc tiện ích (để giải trí, nếu đó là một trò chơi). Ví dụ: chương trình xử lí văn bản là một chương trình ứng dụng.
  - **system program - chương trình hệ thống**: là cần thiết để cho hệ thống hoạt động. Ví dụ: lệnh **mount** là một chương trình hệ thống .
  
  Tuy nhiên sử khác biệt này thường khá mơ hồ và chỉ quan trọng khi chúng ta thật sự chú trọng vào việc phải phân loại chúng.
  </details>

- <details>
  <summary>
  <b>Important parts of the kernel</b>
  </summary>

  Linux Kernel bao gồm các thành phần quan trọng:

  - Process Management
  - Memory Management
  - Hardware device drivers.
  - Filesystem drivers.
  - Network Management.
  - Various other bits and pieces.
  
  Hình sau cho chúng ta thấy một số thành phần quan trọng của Linux Kernel:

  ![img](images/img2.gif)

  Có lẽ các phần quan trọng nhất của Kernel (không thứ gì có thể hoạt động mà không có chúng) là memory management và process management. Memory Mangement sẽ lo việc cấp phát các không gian bộ nhớ và swap các không gian đến process, đến các phần của kernel và đến các bộ nhớ đệm. Process Management sẽ tạo ra các process, và implement tính đa nhiệm bằng cách chuyển đổi process hoạt động trên processor.

  Ở mức độ thấp nhất, kernel (nhân hệ điều hành) chứa một driver thiết bị phần cứng cho mỗi loại phần cứng mà nó hỗ trợ. Vì thế giới đầy rẫy các loại phần cứng khác nhau, số lượng driver thiết bị phần cứng là rất lớn. Thường thì có nhiều phần cứng tương tự nhau nhưng khác nhau về cách điều khiển bằng phần mềm. Sự tương đồng này cho phép có các lớp driver tổng quát hỗ trợ các hoạt động tương tự; mỗi thành viên của lớp đó có cùng giao diện với phần còn lại của kernel nhưng khác nhau ở những gì cần làm để thực hiện các hoạt động đó. Ví dụ, tất cả các driver ổ đĩa đều giống nhau với phần còn lại của kernel, tức là chúng đều có các hoạt động như `khởi tạo ổ đĩa`, `đọc sector N`, và `ghi sector N`.
  </details>

- <details>
  <summary>
  <b>Various Parts of an Operating System</b>
  </summary>

  UNIX và các hệ điều hành giống UNIX (như Linux) bao gồm một Kernel và một số chương trình hệ thống (system program). Ngoài ra, còn có các chương trình ứng dụng (application program) để thực thi công việc. Kernel là phần cốt lõi của hệ điều hành. Thực tế thì Kernel thường bị nhầm lẫn là hệ điều hành nhưng không phải vậy. Hệ điều hành bản thân nó cung cấp nhiều dịch vụ hơn so với Kernel.

  Nó theo dõi các tập tin trên đĩa, khởi động chương trình và chạy chúng một cách đồng thời, cấp phát bộ nhớ và các tài nguyên khác nhau cho nhiều process, nhận các packet và gửi chúng thông qua mạng và tương tự như vậy. Kernel bản thân nó thực hiện rất ít việc, nhưng nó cung cấp các công cụ mà các dịch vụ có thể được xây dựng dựa trên. Ngoài ra nó cũng ngăn chặn bất kì ai truy cập trực tiếp vào các phần cứng, ép họ sử dụng các công cụ mà nó cung cấp. Với cách này Kernel sẽ cung cấp được một số bảo vệ cho người dùng. Các công cụ được cung cấp bởi Kernel được sử dụng thông qua system call.

  Các system program sử dụng tool được cung cấp bởi Kernel để implement một số service được yêu cầu bởi hệ điều hành. System program, và tất cả các loại program khác, chạy *on top* của một Kernel, hay còn được gọi là *user mode*. Sự khác biệt giữa *system program* và *application program* nằm ở mục đích sử dụng:
  - **application program - chương trình ứng dụng**: được thiết kế để thực thi các công việc tiện ích (để giải trí, nếu đó là một trò chơi). Ví dụ: chương trình xử lí văn bản là một chương trình ứng dụng.
  - **system program - chương trình hệ thống**: là cần thiết để cho hệ thống hoạt động. Ví dụ: lệnh **mount** là một chương trình hệ thống .
  
  Tuy nhiên sử khác biệt này thường khá mơ hồ và chỉ quan trọng khi chúng ta thật sự chú trọng vào việc phải phân loại chúng.
  </details>

- <details>
  <summary>
  <b>Virtual Memory</b>
  </summary>

  Linux hỗ trợ **Virtual Memory**, tức là sử dụng một disk như là một phần của RAM và do đó kích thước có thể sử dụng của RAM được tăng lên tương ứng. Kernel sẽ viết nội dung của các block không sử dụng trong bộ nhớ xuống đĩa cứng mà nhờ đó, bộ nhớ có thể sử dụng cho mục đích khác. Khi mà nội dung gốc được yêu cầu, chúng sẽ được đọc lại vào bộ nhớ. Thao tác này được xử lí một cách hoàn toàn vô hình với người dùng; các chương trình trong Linux chỉ thấy một phần lớn hơn của bộ nhớ sẵn sàng để sử dụng và không nhận ra là một phần trong số đó nằm trên đĩa cứng. Tất nhiên, việc đọc và viết lên đĩa cứng sẽ chậm hơn (thậm chí là hàng ngàn lần) so với bộ nhớ thực, do đó chương trình sẽ không chạy nhanh. Phần đĩa cứng được dùng như bộ nhớ ảo được gọi là **không gian swap - swap space**.

  Linux có thể sử dụng một file bình thường trong filesystem hoặc một partition riêng biệt trên đĩa cứng để làm swap space. Swap Partition sẽ nhanh hơn, nhưng sẽ dễ dàng hơn để thay đổi kích thước của một Swap File (không cần phải thay đổi partition trên một đĩa cứng, việc mà có thể phải cài đặt tất cả mọi thứ lại từ đầu). Thế nên, khi chúng ta biết rõ swap space cần thiết là bao nhiêu thì nên sử dụng swap partition, còn nếu không chắc chắn thì chúng ta nên sử dụng swap file trước tiên, sử dụng hệ thống một thời gian để có cảm giác chắc chắn được bao nhiêu swap space là bao nhiêu.

  Chúng ta cũng nên biết rằng Linux cho phép sử dụng nhiều phân vùng swap (swap partition) và/hoặc tập tin swap (swap file) cùng một lúc. Điều này có nghĩa là nếu ta chỉ thỉnh thoảng cần một lượng không gian swap bất thường, ta có thể thiết lập một tập tin swap bổ sung vào những lúc đó, thay vì giữ toàn bộ lượng không gian được phân bổ suốt thời gian.

  Một lưu ý về thuật ngữ hệ điều hành: khoa học máy tính thường phân biệt giữa swapping (ghi toàn bộ quá trình ra không gian swap) và paging (chỉ ghi các phần có kích thước cố định, thường là vài kilobyte, tại một thời điểm). Paging thường hiệu quả hơn, và đó là những gì Linux thực hiện, nhưng thuật ngữ truyền thống của Linux vẫn nói về swapping.
  </details>
</details>

<details>
<summary>
<b>Module 2 - Install VMWare</b>
</summary>

*Chưa có gì phải ghi chú ở đây*
</details>

<details>
<summary>
<b>Module 3 - System Access And File System</b>
</summary>

- <details>
  <summary>
  <b>Important things to remember in Linux</b>
  </summary>
  
  - Linux có một super-user gọi là **root**.
    - root là account có quyền mạnh nhất có thể tạo, chỉnh sửa, xóa các account khác và thay đổi file system của hệ thống.
  - Linux là case-sentitive
    - **ABC** khác với **abc**
  - Linux Kernel không phải là hệ điều hành. Nó là một "chương trình" nhỏ bên trong hệ điều hành Linux sẽ nhận command từ user và pass chúng vào phần cứng hệ thống.
  - Linux phần lớn sử dụng CLI, không phải GUI.
  - Linux rất flexible khi so với các hệ điều hành khác.
  </details>

- <details>
  <summary>
  <b>Linux File System</b>
  </summary>
  
  - File System là một phần mềm hoặc hệ thống được sử dụng để quản lý, tổ chức và lưu trữ dữ liệu trên các thiết bị lưu trữ như đĩa cứng, ổ đĩa USB hoặc thẻ nhớ
  - OS lưu trữ dữ liệu trên ổ đĩa sử dụng một cấu trúc gọi là File System, bao gồm các file, thư mục, và các thông tin cần thiết để truy cập và định vị chúng.
  - Có nhiều loại filesystem khác nhau. Về cơ bản, có nhiều sự cải tiến đối với file system khi ra mắt các hệ điều hành mới, và mỗi file system được đặt một tên khác nhau:
    - E.g ext3, ext4, XFS, NTFS, FAT, etc.
  - Linux filesystem lưu trữ thông tin trong các thư mục phân cấp và file.
    - Filesystem của Linux trông như thế này:
  
    ![img](images/Screenshot%20from%202024-08-19%2020-51-17.png)

  </details>

- <details>
  <summary>
  <b>File System Structure and its Description</b>
  </summary>

  - `/boot`: chứa file được sử dụng bởi bootloader (grub.cfg).
  - `/root`: thư mục home của user root.
  - `/dev`: System devices (eg disk, cdroom, speakers, flashdrive, keyboard etc)
  - `/etc`: Configuration files.
  - `/bin -> /usr/bin`: Everyday user commands.
  - `/sbin -> /usr/sbin`: System/filesystem commands.
  - `/opt`: optional addons applications (các apps không thuộc về OS).
  - `/proc`: Chứa các file, thư mục cho các process đang chạy (bị xóa khi shutdown).
  - `/lib -> /usr/lib`: các file thư viện được viết bằng C cần thiết cho các commands hoặc apps.
  - `/tmp`: thư mục chứa các file tempory.
  - `/home`: thư mục home của user.
  - `/var`: logs của hệ thống.
  - `/run`: các daemons hệ thống chạy rất sớm (e.g systemd và udev) để chứa các file tempory runtime như các file PID.
  - `/mnt`: dùng để mount external filesystem. (e.g NFS)
  - `/media`: dùng để mount cdrom.

  </details>

- <details>
  <summary>
  <b>Navigating File System</b>
  </summary>
  
  Để di chuyển trong UNIX FileSystem, có một số command **quan trọng** cần phải nhớ:
  - `cd - Change Directory`: chuyển thư mục
  - `pwd - Print Working Directory`: Cho biết vị trí hiện tại
  - `ls - listing`: List content
    - `ls -a`: List tất cả (List all).
    - `ls -l`: List đầy đủ thông tin (List long format).
    - `ls -r`: List theo trật tự ngược lại (List with reverse order).
    - `ls -t`: List theo thứ tự thời gian (List with time).
    - `ls -p`: thêm dấu / vào thư mục. (List with indicator-slash)
    - `ls -R`: xem cả cây thư mục (List recursively)
  </details>

- <details>
  <summary>
  <b>What is root</b>
  </summary>
  
  Có 3 loại `root` trong hệ thống Linux mà ta cần phân biệt:
  - Root account: Là một account hay một username trên hệ thống Linux có quyền hạn lớn nhất, được access vào toàn bộ command và file.
  - Thư mục root `/`: Là thư mục đầu tiên trong Linux và còn được biết đến là **root directory** (Lưu ý: đây không phải thư mục user của root).
  - Root home directory: Là thư mục home của user `root`, nằm ở đường dẫn `/root`
  </details>

- <details>
  <summary>
  <b>Creating files and directories</b>
  </summary>
  
  - Tạo file:
    - `touch`: tạo file trống.
    - `cp`: copy file.
      - `cp -R`: copy đệ quy (copy recursively).
    - `vi`: tạo file với trình soạn vi.
  - Tạo thư mục:
    - `mkdir`: tạo thư mục (make directory).
      - `mkdir -p`: tạo cả cây thư mục (make directory parent).
  </details>

- <details>
  <summary>
  <b>Linux File Types</b>
  </summary>

  | Kí hiệu file | Ý nghĩa                     |
  |--------------|-----------------------------|
  | -            | Regular file                |
  | d            | Directory                   |
  | l            | link                        |
  | c            | special file or device file |
  | s            | socket                      |
  | p            | Named pipe                  |
  | b            | block device                |
  </details>

- <details>
  <summary>
  <b>Find files and directories</b>
  </summary>

  Hai lệnh được sử dụng để tìm kiếm file/thư mục:
  - `find`: Tìm kiếm tài nguyên.
    - `find <from_where> -name <search>`: Tìm kiếm tài nguyên theo tên tại from_where.
    - `find <from_where> -type [f | d]`: Tìm kiếm tài nguyên là file (`f`) hoặc thư mục (`d`)
  - `locate`: Tìm kiếm tài nguyên, nhưng là sử dụng cơ sở dữ liệu được lập chỉ mục trước (thường là `/var/lib/mlocate/mlocate.db`) nên rất nhanh.
    - `updatedb`: cập nhật cơ sở dữ liệu chỉ mục.
  </details>

- <details>
  <summary>
  <b>Wildcards</b>
  </summary>

  Wildcards là các kí tự đặc biệt có thể sử dụng để đại diện cho một lớp các kí tự trong các câu lệnh tìm kiếm.

  - `*`: Đại diện cho 0 hoặc nhiều hơn 1 kí tự.
  - `?`: Đại diện cho một kí tự bất kì.
  - `[]`: Đại diện cho một tập hợp các ký tự đơn lẻ mà bạn muốn khớp.
  - `{}`: Đại diện cho một tập hợp các từ hoặc chuỗi (có thể sử dụng để tạo nhiều file)

  Ví dụ:
  - `rm abc*`: xóa tất cả các tài nguyên bắt đầu với `abc`.
  - `touch abc{1..9}-xyz`: tạo 9 file `abc{1 -> 9}-xyz`.
  </details>

- <details>
  <summary>
  <b>Soft and hard links</b>
  </summary>

  **Một số khái niệm cần biết**:

  Trong hệ thống file Linux, một liên kết (link) là một kết nối giữa file name và dữ liệu thực tế trên disk.

  Có hai loại liên kết chính có thể được tạo: "hard" links, và "soft" hay symbolic links. Trước khi tìm hiểu về hard links và symbolic links, có một khái niệm khác cần hiểu rõ là “inode” - một khái niệm cơ bản trong Linux filesystem. Mỗi đối tượng của filesystem được đại diện bởi một inode.

  **Inode**:
  Trong Linux, dữ liệu của các file được chia thành các block. Có nhiều cách tổ chức để liên kết các khối dữ liệu trong một file với nhau, một trong các cách đó là dùng chỉ mục (indexed allocation).

  ![alt text](images/123213218SDHUASHDUS.png)

  Trong một inode có các metadata sau:
  - Dung lượng file tính bằng bytes.
  - Device ID : id của thiết bị lưu file.
  - User ID : id chủ sở hữu của file.
  - Group ID: id nhóm của chủ sở hữu file.
  - File mode : gồm kiểu file và cách thức truy cập file.
  - Timestamps: các mốc thời gian khi: bản thân inode bị thay đổi (ctime, inode change time), nội dung file thay đổi (mtime, modification time) và lần truy cập mới nhất (atime, access time).
  - Link count : số lượng hard links trỏ đến inode. Các con trỏ chỉ đến các blocks trên ổ cứng dùng lưu nội dung file. Các con trỏ cho biết file nằm ở đâu để đọc nội dung.
  - ...
  
  >Inode là một cấu trúc dữ liệu trong hệ thống tệp truyền thống của các họ Unix ví dụ như UFS hoặc EXT3. Inode lưu trữ thông tin về 1 tệp thông thường, thư mục, hay những đối tượng khác của hệ thống tệp tin.
  
  Có hai chú ý trong nội dung inode:
  - Inode không chứa tên file, thư mục.
  - Các con trỏ là thành phần quan trọng nhất: nó cho biết địa chỉ các block lưu nội dung file và tìm đến các block đó có thể truy cập được nội dung file.
  
  **Hard link**:
  Hard Link là các liên kết cấp thấp (low-level links) mà hệ thống sử dụng để tạo các thành phần chính hệ thống file, chẳng hạn như file và thư mục. Liên kết cứng sẽ tạo ra một liên kết trong cùng hệ thống tập tin với 2 inode entry tương ứng trỏ đến cùng một nội dung vật lí (cùng số inode vì chúng trỏ đến cùng dữ liệu).

  Tất cả các hệ thống tệp tin dựa trên thư mục phải có ít nhất một liên kết cứng (link counts từ 1 trở lên) cung cấp tên gốc cho mỗi tệp tin.

  ![alt text](images/SDADUIJSA.png)
  
  **Symbolic Link**:
  - Hầu hết người dùng không muốn tự tạo hoặc sửa đổi các hard links, nhưng các symbolic links là một công cụ hữu ích cho bất kỳ người dùng Linux nào.
  - **Symbolic links** là một file đặc biệt trỏ đến một file hoặc thư mục khác - được gọi là target. Khi được tạo, một symbolic links có thể được sử dụng thay cho target file. Nó có thể có một tên độc nhất, và được đặt trong bất kỳ thư mục nào. Nhiều symbolic links thậm chí có thể được tạo cho cùng một target file, cho phép truy cập target bằng nhiều tên khác nhau.
  
  ![alt text](images/sDSAASD.png)

  - Symbolic link không chứa bản sao dữ liệu của target file. Nó tương tự như một shortcut trong Microsoft Windows: nếu bạn xóa một symbolic link, target sẽ không bị ảnh hưởng. Vì chỉ đơn thuần là một shortcut, symbolic link không dùng đến inode entry. Nó sẽ tạo ra một inode mới và nội dung của inode này trỏ đến tên tập tin gốc.
  - Ngoài ra, nếu target của một symbolic link bị xóa, di chuyển hoặc đổi tên, symbolic link không được cập nhật. Khi điều này xảy ra, liên kết tượng trưng được gọi là "broken" hoặc "orphaned" và sẽ không còn hoạt động như một liên kết.

  Lệnh:
  - `ln`: tạo hard link.
  - `ln -s`: tạo soft link.

  ![img](images/saidjsadsad1273111.png)

  </details>
</details>