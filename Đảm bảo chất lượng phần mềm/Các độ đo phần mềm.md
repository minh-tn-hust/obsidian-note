# Số dòng code (Lines of code)
##### LOCphy: số dòng code logic
##### LOCbl: số dòng trống
##### LOCpro: số dòng code thực sự
##### LOCcom: số dòng comment


# Halsted
>Tính toán độ phức tạp dựa trên việc phân tích mã nguồn thành các token và phân loại các token đó thành hai loại
## Toán tử - operator: bao gồm các keyword và các toán tử
## Toán hạng - operand: bao gồm tên hàm, tên biến và các hằng số

##### Số toán tử phân biệt: n1
##### Số toán hạng phân biệt: n2
##### Tổng số toán tử: N1
##### Tổng số toán hạng: N2

### Độ dài chương trình (N = N1 + N2)
>Chiều dài của chương trình đượ tính bằng tổng số toán tử và số toán hàng

### Độ lớn tập từ vững (n = n1 + n2)
>Kích thước tập từ vuwngx được tính bằng tổng số toán tử và số toán hạng

### Kích thước chương trình (V = N * log2(n))
>miêu tả kích thước cài đặt của một chương trình hay thuật toán

### Độ khó của chương trình (D = (n1/2) * (N2/n2))
>Mức độ tiềm ẩn lỗi của chương trình

### Mức độ chương trình (L = 1/D)
>Đảo ngược của D, càng thấp thì khả năng tiềm ẩn lỗi càng cao

### Công sức cài đặt chương trình (E = V * D)
>Là công sức bỏ ra để cài đặt và độc hiểu mã nguồn

### Thời gian cài đặt chương trình (T = E/18)
>Thời gian cần thiết để cài đặt hoăc hiểu mã nguồn

### Số lượng bug khi bàn giao (B=(E^2/3)/3000)
>Chỉ ra độ phức tạp chung của phần mềm 

---
# Độ đo McCabe
>- Là các số đo dược tính toán dựa trên các đường độc lập tuyến tính trong một chương trình
>- Dựa vào đồ thị luồng điều khiển của chương trình
>- Chỉ số phức tạp của chương trình lớn, càng nhiều nhánh cần thực thi, độ khó chương trình càng cao

#edges: số lượng cạnh
#verticles: số lượng đỉnh
#binaryDecision: số lượng các quyết định rẽ nhánh
#IFS: số lượng câu lệnh IF
#LOOPs: số lượng câu lệnh lặp

### v(G): số lượng các nhánh trong đồ thị luồng điều khiển
##### v(G) = #edges  - #verticles + 2
##### v(G) = #binaryDecision + 1
##### v(G) = #IFs + #LOOPs + 1

# Chỉ số bảo trì được của chương trình (MI)
#MIwoc: chỉ số không có comment
#MIwc: chỉ số có comment
##### MI = #MIwoc + #MIwc 
## MIwoc
```JAVA
MIwoc = 171 - 52 * ln(aveV) - 0.23 * aveG - 16.2 * ln(aveLOC)
```
##### aveV: V trung bình
##### aveG: v(G) trung bình
##### aveLOC: LOCphy trung bình

## MIwc
```java
MIwc = 50 * sin(sqrt(2.4 * perCM))
```
##### perCM: tỉ lệ comment trung bình




