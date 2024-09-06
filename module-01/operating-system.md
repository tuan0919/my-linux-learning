# Khái niệm
Một hệ điều hành hay OS là một chương trình cho phép các phần cứng máy tính có thể tương tác và giao tiếp với các phần mềm trên máy tính. Nếu không có hệ điêu hành, các chương trình máy tính và phần mềm sẽ trở nên vô dụng.

OS là chương trình sau khi được tải vào máy tính bởi một chương trình khởi động (boot program), sẽ quản lý tất cả các chương trình khác trong máy tính. Các chương trình khác được gọi là ứng dụng hoặc chương trình ứng dụng. Các chương trình ứng dụng sử dụng hệ điều hành bằng cách gửi yêu cầu dịch vụ thông qua một giao diện chương trình ứng dụng (API) đã được định nghĩa. Ngoài ra, người dùng có thể tương tác trực tiếp với hệ điều hành thông qua giao diện người dùng, chẳng hạn như ngôn ngữ lệnh hoặc giao diện người dùng đồ họa (GUI).

Một hệ điều hành sẽ thực hiện các dịch vụ sau đây cho chương trình:
- Trong một hệ điều hành đa nhiệm, nơi nhiều chương trình có thể chạy đồng thời, hệ điều hành xác định các ứng dụng nào nên chạy theo thứ tự nào và mỗi ứng dụng được phép sử dụng bao nhiêu thời gian trước khi chuyển cho ứng dụng khác.
- Nó quản lý việc chia sẻ bộ nhớ nội bộ giữa nhiều ứng dụng.
- Nó xử lý việc nhập và xuất dữ liệu từ và đến các thiết bị phần cứng gắn liền, chẳng hạn như ổ cứng, máy in.
- Nó truyền message tới mỗi ứng dụng hoặc người dùng đang tương tác (hoặc đến một operator trong hệ thống) về trạng thái hoạt động và bất kì lỗi nào có thể xảy ra.
- Nó có thể chuyển giao việc quản lý cho các **batch job** (chẳng hạn như thao tác in) và cho phép ứng dụng khởi tạo không phải chịu trách nhiệm thao tác.
- Trong các máy tính có thể xử lí đồng thời. Một hệ điều hành có thể quản lí việc phân chia chương trình để có thể chạy trên nhiều processor tại một thời điểm.