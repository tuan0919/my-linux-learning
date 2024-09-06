# Cách tìm kiếm tập tin

  Hai lệnh được sử dụng để tìm kiếm file/thư mục:
  - `find`: Tìm kiếm tài nguyên.
    - `find <from_where> -name <search>`: Tìm kiếm tài nguyên theo tên tại from_where.
    - `find <from_where> -type [f | d]`: Tìm kiếm tài nguyên là file (`f`) hoặc thư mục (`d`)
  - `locate`: Tìm kiếm tài nguyên, nhưng là sử dụng cơ sở dữ liệu được lập chỉ mục trước (thường là `/var/lib/mlocate/mlocate.db`) nên rất nhanh.
    - `updatedb`: cập nhật cơ sở dữ liệu chỉ mục.