# 14. uniq (Unique)

Lệnh `uniq` cũng là một lệnh khá hữu ích khi dùng để xử lý văn bản.

Hãy giả sử bạn muốn loại bỏ các từ lặp lại trong đoạn văn sau

```sh
reading.txt
book
book
paper
paper
article
article
magazine
```

Bạn có thể sử dụng lệnh `uniq` trong trường hợp này:

```sh

$ uniq reading.txt
book
paper
article
magazine
```

Có thể dùng lên flag `-c` (count) nếu muốn đếm tần suất xuất hiện của các từ lặp lại:

```sh
$ uniq -c reading.txt
2 book
2 paper
2 article
1 magazine
```

Hoặc nếu bạn muốn chỉ lấy giá các từ không lặp lại thì có thể dùng thêm flag `-u` (unique): 

```sh
$ uniq -u reading.txt
magazine
```

Còn ngược lại, nếu bạn chỉ muốn lấy các từ bị lặp lại thì dùng flag `-d` (duplicate):

```sh
$ uniq -d reading.txt
book
paper
article
```

**Chú ý**: Lệnh `uniq` chỉ hoạt động đúng nếu như các từ lặp lại đứng sát nhau.

```sh
reading.txt
book
paper
book
paper
article
magazine
article

$ uniq reading.txt
reading.txt
book
paper
book
paper
article
magazine
article
```

Để vượt qua hạn chế này, thường thì chúng ta sẽ cần kết hợp thêm với lệnh `sort` để sắp xếp các từ lại:

```sh
$ sort reading.txt | uniq
article
book
magazine
paper
```