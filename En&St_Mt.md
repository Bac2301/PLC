# Đọc encoder và chạy step motor
**Để vừa đọc encoder và điều khiển step motor thì phải dùng OB cyclic interrupt**
+ Nó cho phép PLC thực thi một khối chương trình tại các khoảng thời gian cố định, ví dụ 10 ms, 100 ms, 1 s,…

**Mô hình thực tế**


**Kết quả**


**Sơ đồ đấu nối encoder:**

  <img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/baa202e0-eb44-4129-8f49-7c6cca762168" />

  
**Cấu hình PLC:**
+ Bật high speed counter
+ Chọn chế độ đọc (Single, Two phase, A/B counter,..)
+ Điều chỉnh thời gian đọc các chân Channel input filters (0,1-3 milisec) Để loại bỏ nhiễu và tránh đếm sai xung khi đọc tín hiệu
<img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/af7022d6-c920-40a2-a96a-58b3733b4494" />
<img width="300" height="150" alt="image" src="https://github.com/user-attachments/assets/5e62a916-31c4-448b-95d9-e40acae59497" />
<img width="300" height="150" alt="image" src="https://github.com/user-attachments/assets/32b805c8-8c3b-459c-9c03-dfc183ab719c" />

**Chương trình PLC:**

<img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/cbfc3ae7-3d0f-4278-9770-45c26c98fb31" />

**Tính toán tốc độ động cơ:**   
+ Xung đọc được từ encoder gán cho "current xung"
+ "delta xung" = "last xung" - "current xung"
+ Đổi "delta xung" sang "xung/s" (bộ ob cyclic đặt 100ms thì nhân thêm 10 để được 1s)
+ Đổi xung/s sang xung/p (đổi xung từ giây sang phút)
+ Đổi xung/p từ Dint sang Real thu được xung real
+ Lấy xung xung real / độ phân giải của encoder -> thu được tốc độ thực tế (Vòng/phút)
+ Cuối chương trình đọc giá trị của last xung

<img width="500" height="700" alt="image" src="https://github.com/user-attachments/assets/943df9f0-a31d-415a-86ec-41fb650015e5" />

**Sơ đồ đấu nối Step Motor:**

<img width="500" height="350" alt="image" src="https://github.com/user-attachments/assets/e2cce5b6-f225-4899-898c-7ecacc812a8e" />

**Cấu hình PLC:**
+ Bật xuất xung điều khiển
+ Đặt 2 chân xuất xung, và xuất tín hiệu hướng
+ Tạo trục định vị TO_PositioningAxis (technology object / add new object / motion control / TO_PositioningAxis)
	+ Trong Axis (DB1):
      + Đặt đơn vị tính là pulse (xung)
      + Harware interface chọn pulse 1 đã tạo trước từ đầu
      + Đặt tốc độ mặt định, thời gian tăng tốc, thời gian dừng khẩn cấp
      + Pulse output (chân xuất xung PTO), Direction output (chân điều khiển chiều xoay thuận nghịch của động cơ)


<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/83c48abf-0e4e-420d-a706-acc09f30595b" />

**Chương trình PLC:**
*Chỉ có quay thuận nghich với đặt tốc độ động cơ*

<img width="750" height="500" alt="image" src="https://github.com/user-attachments/assets/8328a3f6-50a7-4ddf-9eec-e5a8761ec8a3" />

