# Độ đo Module
>Là mức độ một hệ thống có thể được chia thành các pơhaanf khác nhau và chúng kết nối lại với nhau
##### Cohesion: số lượng lời gọi bên trong một module
##### Coupling: số lượng lời gọi giữa các module
>Thiết kế tốt phải dựa trên hai tính chất
>- High cohesion
>- Low coupling

##### Fan-in(M): Số lượng lời gọi hàm bên trong module M
##### Fan-out(M): Số lượng lời gọi tới M bên ngoài module M
> Một module càng độc lập nêu Fan-in càng nhiều và Fan-out càng ít

## Chỉ số HK cho phép tính mức độ mô-đun hóa của các chương trình
##### HK = SLOC * (fan-in * fan-out)^2
#SLOC: số dòng code không tính comments và dòng trống

# Độ đo Chidamber và Kemerer
##### WMC: Số phương thức trên một lớp
>Tính toán đô phức tạp của một lớp liên quan đến số phương thức của lớp đó hoặc tổng số độ phức tạp của các phương thức trong lơp (Độ phức tạp ở đây là độ phức tạp McCabe)

##### RFC: Chỉ số phản hồi của một lớp
>Tổng tất cả các phương thức có thê gọi để phản hồi cho một thông điệp tới đối tượng của lớp hoặc một phương thức nào đó của lớp

###### Cách tính
1. Xác định tát cả các phương thức bên ngoài được gọi bởi các phương thức bên trong lớp
2. Tạo một tập hợp các phương thức bên ngoài và các phương thức của lớp gọi là tập #RS 
3. #RFC được tính bằng kích thước của tập #RS

##### LCOM: Sự thiếu kết dính cả các phương hức trong lớp
>Đo mức độ không tương tự nhau / sự khác nhau của các phương thức trong một lớp dựa trên các thuộc tính của lớp
>Các method được gọi là kết nối với nhau nếu như chúng sử dụng cùng thuộc tính của lớp
###### Các tính
#LCOM = #P - #Q nếu như #P > #Q và bằng **0** ngược lại
- #P : số cặp phương thức riêng biệt trong lớp không chia sẻ biến
- #Q : số cặp phương thức riêng biệt trong lớp có chia sẻ biến

##### CBO: Sự kết nối giữ các đối tượng
>Tính số lượng các lớp có kết nối với lớp được tính
>- Kết nối ở đây là số lượng lớp có liên quan không có trên cây thừa kế của lớp
>- Bất kì sự liên quan nào đến một lớp khác của lớp được coi như là một sự phụ thuộc vào bên ngoài
##### DIT: Độ sau trên cây kế thừa
>Độ sau của một lớp trên cây kế thừa tính bằng **số lượng bước tối đa từ nút của lớp đến gốc của cây, đo bằng số lớp cha**

##### NOC: Số lượng lớp con
>Là một chỉ số tính số lượng lpows con trung gian từ một lớp trên cây kế thừa


# Độ đo Module
##### #CE: độ đo mối quan hệ hướng ra ngoài của một lớp với các lớp khác, **được tính bằng cách tính số lượng các lớp trong một gói phụ thuộc vào các lớp của các gói khác**

##### #CA: tính toán dựa trên độ lệ thuộc đến gói đó, **dduowjc tính bằng số lớp từ những gói khác lệ thuộc vào các lớp trong gói được tính**

##### #I: sử dụng để đo lường một cách tương đối mực độ nhạy cảm của một lớp đối với thay đổi
###### Cách tính: #I = #CE / ( #CE + #CA)

##### #A: Mức độ trừu tượng hóa thể heienj của một gói có phần
###### Cách tính: #A = #TA / ( #TA + #TC)
- #TA là số lượng các lớp trừu tượng trong gói
- #TC là số lượng các lớp cụ thể có trong gói


