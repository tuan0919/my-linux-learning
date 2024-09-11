## Áp dụng kỹ thuật piping trong khi filtering

Do các câu lệnh trong Linux thường chỉ đảm nhiệm một công việc nhất định, nên có một số trường hợp ta cần kết hợp nhiều câu lệnh mới hoàn thành được công việc. Chính vì vậy, khi filtering ta có thể sử dụng kỹ thuật piping để các câu lệnh có thể liên kết với nhau dễ dàng hơn.

### Các câu lệnh dùng để filtering
Dưới đây liệt kê một số câu lệnh thường được sử dụng nhiều nhất cho kỹ thuật `Filtering` trong **Linux**.

**Câu lệnh _cat_ và _tac_**

Mặc dù không có tác dụng là lọc dữ liệu, nhưng đây là 2 câu lệnh cực kì hữu hiệu để lấy dữ liệu từ file, phục vụ cho việc đọc dữ liệu. Nội dung của file có thể được in ra màn hình mà không cần phải mở file bằng bất cứ một trình soạn thảo văn bản nào. Điểm khác biệt là `cat` sẽ in file từ dòng đầu tiến dòng cuối cùng, còn `tac` sẽ in theo thứ tự ngược lại với `cat`.

(Với `cat` khi dùng `-n` thì sẽ in kèm theo cả số dòng).

>Hai lệnh `cat` và `tac` chỉ đơn giản là in cho ta nội dung của file

**Câu lệnh _head_ và _tail_**

Hai câu lệnh này tương tư như nhau về cách sử dụng, chỉ có khác nhau một điều là `head` lọc dữ liệu từ trên xuống còn `tail` thì lọc từ dưới lên. Mặc định 2 câu lệnh này đều lấy 10 dòng dữ liệu, hoặc có thể chỉ định số dòng muốn lấy bằng tùy chọn `-n`.

Với việc kết hợp `head` cùng với `tail` thông qua `piping`, dữ liệu được sử dụng cho câu lệnh sau sẽ được lấy thông qua câu lệnh trước. như vậy nếu dùng câu lệnh `cat .bashsrc | head -n 7 | tail -n 2 ` thì kết quả cuối cùng sẽ là 2 dòng 6 và 7 của file `.bashrc`. Với việc dùng `-c` thay cho `-n`, đơn vị tính sẽ chuyển về số byte kí tự thay vì số dòng.

>`head` và `tail` sẽ được dùng khi chúng ta có số lượng dữ liệu với rất nhiều dòng nhưng lại chỉ muốn lấy một số dòng cụ thể và liên tiếp nhau

**Lệnh _sort_ và _uniq_**

Lệnh sort có tác dụng sắp xếp các dòng dữ liệu theo một thứ tự nhất định (mặc định sẽ sắp xếp theo thứ tự bảng chữ cái). Lệnh `uniq` thường dùng chung với `sort`, có tác dụng loại bỏ các kết quả trùng lặp sau khi sắp xếp.

>`sort` và `uniq` có tác dụng giúp cho việc kiểm kê các dạng dữ liệu tương tự nhau được dễ dàng hơn.

**Lệnh cut**
Thay vì lấy các dòng dữ liệu như `head` và `tail`, `cut` có tác dụng để lấy các cột dữ liệu (thường là dữ liệu dạng bảng)
- Tùy chọn `-f` để chỉ định thự tự của cột sẽ lấy (mặc định sẽ lấy tất cả các cột)
- Tùy chọn `-d` để định nghĩa separator (mặc định sẽ dùng ký tự TAB)

```bash
cat file_test
id name
1 apple
2 orange
3 watermelon
4 mango
cat file_test | tail -n 4 | cut -f 2 -d ' '
apple
orange
watermelon
mango
```

Có thể lấy nhiều cột như ví dụ sau:

```bash
cat file_test
id name amount
1 apple 6
2 orange 7
3 watermelon 8
4 mango 9
cat file_test | tail -n 4 | cut -f 2,3 -d ' '
apple 6
orange 7
watermelon 8
mango 9
```

>`cut` là lệnh cực kỳ hữu ích trong trường hợp thao tác với dữ liệu dạng bảng

**Lệnh _less_ và _more_**
Trong trường hợp cần phải đọc toàn bộ dữ liệu từ một file nhưng lại không muốn mở file đó lên bằng một trình soạn thảo nào đó, ta có thể sử dụng lệnh `less` hoặc `more` để phân trang file cần đọc. Điểm khác biệt giữa `less` và `more` là `less` cho phép cuộn ngược lên trang dữ liệu đã đọc, còn `more` thì chỉ có thể đọc từ đầu đến cuối. Có một cách khác khi đọc dữ liệu kiểu này là có thể dùng lệnh cat để in toàn bộ dữ liệu ra màn hình, tuy nhiên trong môi trường **console** nếu không hỗ trợ scrolll bar thì không thể xem hết được nội dung file nếu file quá dài.

>`less` và `more` thường được dùng để phân trang dữ liệu

**Lệnh _grep_**

Lệnh này có tác dụng tìm kiếm trong file stream các dòng dữ liệu có chứa một cụm từ cụ thể.
- Tùy chọn `-v` sẽ đảo ngược kết quả tìm kiếm, dữ liệu sẽ là các dòng không chứa cụm từ nhập vào.
- Tùy chọn `-c` sẽ đếm số dòng xuất hiện của cụm từ truyền vào.
- Tùy chọn `-l` sẽ tìm kiếm mà không phân biệt chữ hoa và chữ thường.

> Lệnh `grep` thường được dùng cho công việc tìm kiếm dữ liệu từ file