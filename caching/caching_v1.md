# CACHING - PHẦN 1

## 1. Những concept cơ bản
- Caching là hành động lưu trữ lại kết quả của action tốn thời gian để phục vụ lại để sử dụng nhanh hơn
- Tiêu chí để xem có cần cache hay không:
  + Tốn nhiều time/resource
  + Kết quả dừng lại được nhiều lần
  + Ví dụ: 
    + Data get từ DB mất 500ms nhưng chỉ request 1 lần trong 1 trong ít ai vào -> ko cần cache
    + Đoạn CSS build mất 100ms nhưng tất cả user  cần phải load -> cần cache


## 2. Bức tranh lớn về caching

![img.png](../img_guide/img.png)

- 4 layer khi caching 1 application là:
  + Client 
  + Proxy 
  + Application
  + Database

## 3. Các level caching

### 3.1 Level 1 : Một web monolith với 1 server
- Một web monolith, chạy trên 1 server, render data html chủ yếu là các trang tin tức, crud, Data còn khá nhỏ
- Những điều làm cho web bị chậm:
  + một trang html có thể được gender bởi 10-40 query DB, độ trễ 2-3s
  + Media data (image/video) trên trang load chậm làm trang bị trắng 2-10s

- Cách tối ưu:
  + ![1.png](../img_guide/1.png)
  + ![2.png](../img_guide/2.png)