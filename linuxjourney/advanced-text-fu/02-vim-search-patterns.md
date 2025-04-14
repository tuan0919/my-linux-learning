# 2. Vim Search Pattern

Trong vim, để tìm kiếm theo một mẫu nào đó bạn có thể dùng lệnh `/` rồi nhập mẫu mà bạn cần tìm kiếm. Một khi bấm enter thì bạn có thể bấm "n" để tìm từ khớp tiếp theo hoặc "N" để quay về từ trước đó trong kết quả tìm kiếm.

```sh
My pretty file is very pretty.
/pretty
```

:bulb: Sẽ tìm các từ "pretty" trong đoạn văn bản.

```sh
My pretty file is very pretty.
?pretty
```

:bulb: Lệnh `?` sẽ tìm kiếm theo chiều ngược lại, thế nên trong trường hợp này từ pretty phía cuối văn bản sẽ được tìm thấy đầu tiên.