# CACHING - PHẦN 1

1. Những concept cơ bản
- Caching là hành động lưu trữ lại kết quả của action tốn thời gian để phục vụ lại để sử dụng nhanh hơn
- Tiêu chí để xem có cần cache hay không:
  + Tốn nhiều time/resource
  + Kết quả dừng lại được nhiều lần
  + Ví dụ: 
    + Data get từ DB mất 500ms nhưng chỉ request 1 lần trong 1 trong ít ai vào -> ko cần cache
    + Đoạn CSS build mất 100ms nhưng tất cả user  cần phải load -> cần cache


2. Bức tranh lớn về caching

![img.png](../img_guide/img.png)

- 4 layer khi caching 1 application là:
  + Client 
  + Proxy 
  + Application
  + Database
3. Chi tiết từng layer caching

- 