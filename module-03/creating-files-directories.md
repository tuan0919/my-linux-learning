# Cách tạo file và thư mục trong Linux

- Tạo file:
  - `touch`: tạo file trống.
  - `cp`: copy file.
    - `cp -R`: copy đệ quy (copy recursively).
  - `vi`: tạo file với trình soạn vi.
- Tạo thư mục:
  - `mkdir`: tạo thư mục (make directory).
    - `mkdir -p`: tạo cả cây thư mục (make directory parent).

# Kí hiệu tập tin

| Kí hiệu file | Ý nghĩa                     |
|--------------|-----------------------------|
| -            | Regular file                |
| d            | Directory                   |
| l            | link                        |
| c            | special file or device file |
| s            | socket                      |
| p            | Named pipe                  |
| b            | block device                |