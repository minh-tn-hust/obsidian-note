# Tài nguyên sử dụng
## CPU Usage
>Là phần trăm tổng dung lượng CPU tại một thời điểm nhất định
>Mức sử dụng CPU là một số liệu để định lượng tải của bỗ xử lý bằng 

##  Memory Footprint
>Lượng bộ nhớ mà chương trình tham chiếu đến khi chạy

## Execution Time
>Thời gian trôi qua từ khi bắt đầu kiểm tra sử dụng nhiều tài nguyên đến khi hoàn thành

# CUP usage measurement
>Đo mức sử dugnj CPU trên Android

# Memory footprint measurement
>Sử dụng các lệnh hỗ trợ bởi Android và Xcode

# Total data transferred
>Tổng dữ liệu được truyền tải ở trên network

# Execution time
>Ghi nhận các lệnh trong ứng dụng và log ra các khoảng thời gian thực thi để hoàn thành công việc

## Thiết bị được lựa chọn
- Thiết bị cao cấp / Thiết bị cấp thấp
- Ứng dụng được thiết kế là ứng dụng một trang có ba nút
- Mỗi nút bắt đầ một resource-intensive test và ghi lại thời gan thực thi kiểm tra
- Tất cả các ứng dụng được phát triển với cấu hình mặc định của chúng, ngôn ngữ lập trình thông thường và sử dụng IDE được đề xuất
- Các bài test: CPI - intensive test, memory-intensive tét, network intensive test

### CPU - intensive test
> Bài kiểm tra chuyên sâu về CPU để đánh giá việc sử dụng tại nguyên và hiệu suất, đặc biệt tập trung vào việc sử dụng CPU của ứng dụng

	Bài kiểm tra được thiết kế để tìm các số nguyên tố

### Memory-intensive Test
>Bài toán liên quan tới đồ thị, tìm tất cả chu trình của một đồ thị lớn
>Việc truyển khai thuật toán Floyd-Warshall đã được sử dụng để lấy ma trận liền kề. Thử nghiệm đã được tùy chỉnh đê đẩy mức tiêu thủ bộ nhớ đến giới hạn của nó và đồng thời nó có thể hoàn thành được

### Network-intensive Test
>Sử dụng các lời gọi resFull API

## Toognr kết:
### Kết quả chung
 - React Native có thời gian thực hti cao hơn đáng kể so với các phương pháp khác trong CPU - intensive test ở cả 2 nền tảng
 - Lớp thiết bị có ảnh hướng lớn đến thời gian thực thi của tất cả phuowgn pháp phái triển trong CPU intensive test trên cả hai nền tảng Android và IOS
 - Mức độ sử dụng CPUI cao 
 - Lóp thiết bị có ảnh hướng đến thời gian thực thi
### Ảnh hưởng của thiết bị tới bài test
- Yếu tố về phần cứng
	- Phần cứng mạnh hơn -> Nhanh hơn
	- Phần cứng yếu hơn
- Yếu tố thứ 2 nằm ở tuổi của phần mềm
- Bài test Network, Flutter gây ra không ổn định là do
	- Trong quá trình thực hiện request HTTP, Flutter có giữ kết nối các lời gọi, khi tăng lên thì sẽ gây ra nghẽn. Đối với Android hỗ trợ lời gọi nhiều hơn


# Đánh giá của các nhà phát triển
## Số dòng code:
- Dòng mã (LOC) ước tính nỗ lực của việc viết một chương trình cũng như khả năng bảo trì khi một chương tình được viết
- SLOC : số dòng mã nguồn khoongbao gồm nhận xét và dòng trống
- LLOC: đo số lượng các câu lệnh có thể thực thi

## Độ phức tạp chu trình (Cyclomatic):
- Sử dụng để đô đô phức tạp của đoạn mã
- Dựa trên chuyển đổi mã nguồn của chướng trình thành một đồ thị có hướng
- Chuyển mã nguồn -> đồ thị -> tính được độ phức tạp

## Thời gian build
- Quá trình thực hiện chuyển đỏi mã nguồn thành phên bản có thể chạy được


```js
const 
```






