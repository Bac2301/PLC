# Đọc nhiệt độ bằng PTA9B01 và PT100
## Đọc nhiệt độ bằng PTA9B01

**Thiết bị:**
+ PTA9B01
+ Module mở rông CM1241 RS485
+ PLC S7 1200
  
**Đấu nối:**

<img width="600" height="350" alt="image" src="https://github.com/user-attachments/assets/bc690520-8c47-4fdf-a927-ce92ee5f44f5" >
<img width="739" height="305" alt="image" src="https://github.com/user-attachments/assets/cdc728c7-9873-4108-96e2-1fe66b46bd61" />

**Chương trình:**

<img width="838" height="614" alt="image" src="https://github.com/user-attachments/assets/29963ac5-4ffa-413c-bce4-2dde86ee1e0d" />

## Đọc nhiệt độ bằng PT100

**Thiết bị:**
+ PT100
+ Bộ chuyển đổi nhiệt
+ Điện trở 500 ohm
+ PLC s7 1200

**Đấu nối:**

<img width="600" height="455" alt="image" src="https://github.com/user-attachments/assets/223e0e65-5a5e-43f6-b90d-d711c318bb0e" />

**Giải thích:**

+ PT100 xuất giá trị analog dòng từ 4-20mA  
+ PLC S71200 có chân đọc analog nhưng chỉ đọc được điện áp từ 0-10V. Phải cần có module analog mở rộng mới đọc được dòng từ 4-20mA.
+ Để đọc mà không cần module mở rộng thì dùng một điện trở 500 ohm
+ Vout = I*R 
+ -> 10V = 20mA *R
+ -> R = 10/(20/10^-3) = 500 ohm

**Chương trình:**

