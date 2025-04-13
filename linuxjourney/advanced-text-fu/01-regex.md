# 1. regex (Regular Expression)

Biểu thức chính quy là một công cụ mạnh mẽ để thực hiện tìm kiếm dựa trên một mẫu nào đó. Nó sử dụng các ký hiệu đặc biệt chẳng hạn như ký tự đại diện `*` mà chúng ta đã gặp trước đó.

🔍 Chúng ta sẽ tìm hiểu một số biểu thức hay dùng, nhiều trong số chúng được xem là quy chuẩn chung trong nhiều ngôn ngữ lập trình khác nhau.

Chúng ta sẽ sử dụng đoạn văn sau để thử nghiệm:

```sh
sally sells seashells 
by the seashore
```

## 1. Bắt đầu một dòng với ^

```
^by
```

:bulb: Sẽ khớp với dòng bắt đầu với từ by, mà cụ thể là "by the seashore".

## 2. Kết thúc một dòng với $

```sh
seashore$
```

:bulb: Sẽ khớp với dòng kết thúc với từ seashore, cụ thể là "by the seashore".

## 3. Khớp bất kỳ kí tự nào với .

```sh
b.
```

:bulb: Sẽ khớp với từ b với kí tự bất kì theo sau, cụ thể là "by".

## 4. Ký hiệu ngoặc với []

```sh
d[iou]g
```

:bulb: Sẽ khớp với các kí tự nằm trong dấu ngoặc `[]`, cụ thể là "dig", "dog", "dug"

Ngoài ra, kí tự `^` khi sử dụng trong dấu ngoặc `[]` sẽ khớp với bất kì kí tự nào trừ kí tự được liệt kê.

```sh
d[^i]g
```

:bulb: Sẽ khớp với bất kỳ kí tự nào không phải `i`, cụ thể là "dog", "dug" nhưng không phải "dig".

Dấu `[]` cũng có thể được dùng để liệt kê một khoảng ký tự sẽ dùng để so khớp.

```sh
d[a-c]g
```

Sẽ khớp với "dag", "db" và "dcg".

