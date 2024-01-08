## Cách 1. Index:
- Bản chất quá trình index là việc chuyển đổi một hoặc nhiều column sang table mới (Hệ thống sẽ quản lý table này)
- Các tính chất:
    + Table index đc sắp xếp thứ tự, Giá trị của column là giá trị của một/nhiều column được đánh index
    + Tìm kiếm nhanh hơn đối với các column được đánh index
    + Mỗi index được ánh xạ sang một hoặc nhiều row trong table chính
    + Có thể index nhiều cột một lúc
    + Index chỉ hiệu quả với những query có where condition trên column index
  
## Cách 2: Partition
-  Các tính chất:
   + Chia table thành các sub-table nhỏ hơn dựa trên các điều kiện tìm kiếm
   + Từ đó giảm không gian tìm kiếm -> Tốc đọ scanning nhanh hơn -> tăng performance khi query
   + Phù hợp với các table có số lượng record cực lớn
   + Vì table được phân chia làm nhiều sub-table ên cần biết chính xác record muốn tìm kiếm ở sub-table nào để tận dụng lợi thế của partition
      + Do vậy cần dùng partition-key (có thể là khoảng tgian 2020, 2021) hoặc giá trị số lượng ít : Giới tính Nam nữ
   + Ngoài ra sub-table cũng đc coi là 1 table -> Có thể index cho chúng:
