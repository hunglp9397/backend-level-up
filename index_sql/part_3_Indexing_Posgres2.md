# Indexing part 2

## 1. B-tree index
- Sử dụng cấu trúc dữ liệu là Binary tree để thực hiện lưu trữ và tìm kiếm


### 1.1 Thử phân tích câu query sau:
```roomsql
    EXPLAIN ANALYZE SELECT * FROM ENGINEER WHERE first_name = 'Dominique' AND last_name = 'Rice';
```

![11.png](/img_guide/11.png)

- Ta thấy vẫn là sequence scan với filter cho câu điều kiện : WHERE first_name = 'Dominique' AND last_name = 'Rice';
- Tiến hành đánh index cho hai columne là first_name và lastname:
```roomsql
CREATE INDEX idx_engineer_firstname_lastname ON ENGINEER(first_name, last_name);
```
![12.png](/img_guide/12.png)
- Nhìn vào thông số execution time, khác bọt được thể hiện rõ. Tốc độ query sau khi index tăng chóng mặt khoảng... 90 lần


### 1.2 Thử một câu query khác như sau:
````roomsql
EXPLAIN ANALYZE SELECT * FROM ENGINEER WHERE first_name = 'Dominique' AND last_name LIKE '%a%';

````
![13.png](/img_guide/13.png)
- Plan có vẻ rắc rối hơn nhưng có index scan, execution time vẫn ổn. Đi qua plan chút xem nó hoạt động thế nào
- _Chú ý cách đọc plan sẽ đi từ trong ra ngoài, không phải từ trên xuống dưới:_
  + Step đầu tiên dễ dàng nhận thấy là index scan với điều kiện first_name = Dominique trước, lọc ra đc 58 rows.
  + Sau đó thực hiện filter với cả 2 điều kiện first_name = Dominique và last_name LIKE %a%, loại bỏ được 43 rows.
  + Kết quả thu được 15 rows với thời gian chưa đến 1 ms.

### 1.3 Thử một câu query khác như sau:
````roomsql
EXPLAIN ANALYZE SELECT * FROM ENGINEER WHERE first_name LIKE '%v%' AND last_name = 'Parker';
````

- Kết quả:
  ![14.png](/img_guide/14.png)
- Ta thấy là : execution time tăng bất thường, không có index scan mà là seq scan
- **Từ đó, rút ra vài chú ý khi sử dụng B-Tree index:**

  + Không có tác dụng khi tìm kiếm text sử dụng điều kiện LIKE '%%'. Index nữa index mãi thì tốc độ tìm kiếm.. không thay đổi mà tốc độ insert còn tăng lên.
  + Với composite index, WHERE condition cần match full value hoặc match mostleft column để đạt hiệu quả tối đa.