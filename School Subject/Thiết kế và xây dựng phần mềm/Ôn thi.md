![[320685628_688856256058158_3047664685080728330_n 1.jpg]]
# Mô hình phát triển phần mềm
## Mô hình thác nước/tuyến tính
> Các bước thực hiện 
> - Yêu cầu, phân tích và định nghĩa
> - Hệ thống và thiết kế phần mềm
> - Thực hiện và kiểm thử đơn vị
> - Tích hợp và thử nghiệm hệ thống
> - Cài đặt
> - Hoạt động và bảo trì

### Mô tả
- Mô hình thác nước là mô hình áp dugnj theo tính tuần tự của các giai đoạn phát triển phần mềm
- Giai đoạn sau chỉ được thực hiện khi giai đoạn trước đã kết thúc
- Không được quay lại giai đoạn trước để xử lý các thay đổi trong yêu cầu

## Mô hình thác nước lặp lại
> Các bước thực hiện 
> - Yêu cầu, phân tích và định nghĩa
> - Hệ thống và thiết kế phần mềm
> - Thực hiện và kiểm thử đơn vị
> - Tích hợp và thử nghiệm hệ thống
> - Cài đặt
> - Hoạt động và bảo trì
> Chỉ khác ở việc các bước sau sẽ feedback ngược lại cho các bước trước
### Mô tả
Là mô hình thác nước nhưng kết hợp các bước lặp để có thể quay lại các bước trước và xử lý các thay đổi trong yêu cầu
## Mô hình lặp lại
> Mỗi lần lặp lại tạo ra một tệp thực thi và được phát hành
> 1. Ban đầu
> 2. Lập kế hoạch
> 3. Yêu cầu
> 4. Phân tích và thiết kế
> 5. Thực hiện
> 6. Kiểm thử
> 7. Triển khai
> 8. Đánh giá

## Mô hình nguyên mẫu
>1. Thu thập yêu cầu
>2. Thiết kế và xây dựng mẫu 
>3. Đánh gia nguyên mẫu với khách hàng
>4. Xây dựng/sử đổi nguyên mẫu
## Mô hình xoắn ốc
>1. Giao tiếp khách hàng
>2. Lập kế hoạch
>3. Phân tích rủi ro
>4. Kỹ thuật
>5. Xây dựng và phát hành
>6. Đánh giá của khách hàng
>7. Quy lại bước 1
### Mô tả
- Là mô hình kết hợp giữa các tính năng của mô hình nguyên mẫu và mô hình thác nước
- 

## Mô hình gia tăng
>Các yêu cầu được chia nhỏ thành nhiều thành phần
>Chu kỳ được chia thành các module nhỏ, dễ quản lý
>Mỗi module sẽ đi qua các yêu cầu về thiết kế, thực hiện, ... như 1 vòng đời phát triển thông thường


## Mô hình Agile
> Được tạo ra dựa tren 2 mô hình : Lặp và Tăng dần


![[320685628_688856256058158_3047664685080728330_n 2.jpg]]
# Phân tích sử dụng các biểu đồ
## Mô hình hóa (pha phân tích)
### Biểu đồ usecase
#### Vai trò: sử dụng để mô tả các chức năng của phần mềm về các trường hợp sử dụng
Sau khi có ca sử dụng, chúng ta sẽ sử dụng đặc tả usecase để có thể mô tả quá trình các hoạt động xảy ra trong usecase đó, đầu vào đầu ra của usecase là gì, các điều kiện tiên quyết, các hậu điều kiện phải làm sau khi thực hiện usecase. Bên cạnh đó còn xác định các luồng thực thi phụ, các hành động xảy ra khác với luồng hành động chính của usecase
#### Kĩ thuật xây dựng
Đầu tiên trích xuất các tác nhân tham gia vào hệ thống (chú ý các danh từ trong phần mô tả vấn đề)
Tiếp theo đó trích xuất các ca sử dụng (chú ý vào các động từ được mô tả)
Tìm các mối quan hệ giữa các tác nhân, giữa các usecase với nhau


### Biểu đồ hoạt động
#### Vai trò: sử dụng để có thể nắm bắt các hoạt động xảy ra trong một ca sử dụng
Sau khi có đặc tả ca sử dụng, sử dụng đặc tả ca sử dụng để có thể sinh ra được biểu đồ hoạt động. Một biểu đồ hoạt động tương ứng với một ca sử dụng, mô tả lại các hành động xảy ra trong ca sử dụng bao gồm cả luồng chính và luồng phụ của ca sử dụng đó
#### Kĩ thuật xây dựng
Dựa trên đặc tả usecase để thực hiện triển khai biểu đồ activity, đưa ra các bên liên quan (các vùng tổng quát) tham gia vào hoạt động của usecase và thực hiện xây dựng chuỗi hành động tương tác giữa các bên với nhau mô tả lại luồng hoạt động của usecase

## Thiết kế kiến trúc (pha thiết kế)
### Biểu đồ Sequence Diagram
#### Vai trò: sử dụng để mô tả chi tiết luồn sự kiện xảy ra bên trong usecase, xác định các đối tượng tham gia vào usecase và mô hình hóa thông điệp giữa các đối tượng
Sau khi có biểu đồ hoạt động, để có thể cụ thể hơn luồng hoạt động chúng ta sử dụng biểu đồ SD và thêm vào các đối tượng tham gia và thông điệp giữa chúng
#### Kĩ thuật xây dựng
Dựa vào biểu đồ hoạt động, xác định các đối tượng tham gia vào luồng hoạt động của mỗi vùng (boundary, controller, entity), thực hiện hiện mô tả lại luồng hoạt động sử dụng các thông điệp gửi qua lại giữa các đối tượng với nhau theo trình tự nhất định
### Biểu đồ lớp phân tích
#### Vai trò: đưa ra thiết kế lớp tham gia vào luồng hoạt động của usecase và các thông điệp được tạo ra để có thể xây đựng được biểu đồ các lớp tham gia, mối quan hệ giữa các lớp với nhau
Sau khi có biểu đồ sequence, chúng ta có thể xác định được các đối tượng tham gia vào quá trình hoạt động, mỗi đối tượng đó tương ứng với một lớp trong biểu đồ lớp phần tích. Kết hợp với thông điệp được gửi ở biểu đồ sequence để tạo ra phương thức của các lớp. Kết hợp các lớp thực thể để tạo ra thuộc tính
#### Kĩ thuật xây dựng
Dựa vào biểu đồ sequence/comunicate, ánh xạ các đối tượng xuất hiện trong biểu đồ sequence thành một lớp có trong biểu đồ lớp phân tích. Chuyển đổi các thông điệp gửi qua lại giữa các đối tượng thành các phương thức có trong các lớp. Thực hiện hợp nhất các thực thể có trong biểu đổ sequence để tạo thành các thuộc tính. Sau đó là hợp nhất các lớp để có thể tối giản nhất.
