# Phân chia lớp tương đương
>Chia miền dữ liệu đầu vào của chương trình thành các lớp tương đương

Một lớp tương đương được định nghĩa là
- Tập hợp các điểm dữ liệu cho phép chương trình có cùng 1 hành xử
- Tập các dữ liệu trong lớp là tương đương nhau
## Kiểm thử lớp tương đương

#### #Step1: Xác định các phân lớp tương đương từ yêu cầu đặc tả của chương trình

#### #Step2: Với mỗi lớp tươn đương, lấy ra dữ liệu đặc trung để xây dựng test case


# Phân tích giá trị lớp biên
>Là phương pháp phụ trợ cho phân chia lớp tương đương khi thiết kế các ca kiểm thử

## Cách làm

#### #Step1: Xác định các phân lớp tương đương

#### #Step2: Xác định giá trị biên của các lớp tương đuong

#### #Step3: Tạo các ca kiểm thử cho mỗi một giá trị biên, một giá trị bé hơn biên, và giá trị lớn hơn biên

# Bảng quyết định
>Là công cụ xuất xác để mô tả các yêu cầu có quan hệ chặt chẽ với nhau trong một hệ thống

![[Pasted image 20230228235150.png]]

# Kiểm thử trạng thái
>- Áp dụng khi một ứng dụng đưa ra các output khác nhau với cùng một đầu vào, phụ thuộc vào những gì đã diễn ra ở trạng thái trước đó
>- Hệ thông có thể trong nhiều trạng thái khác nhau, và các lần chuyển trạng thái từ trạng thái này và trạng thái khác được quyết định bởi các luật
>- Phải quyết định trạng thái, sư kiện, hành động và chuyển trạng thái cần được test

## Các thuật ngữ cơ bản
- Các trạng thái mà hệ thống có thể chiếm
- Các chuyển trạng thái (transition) từ một trạng thái này sang một trạng thái khác
- Các sự kiện gây ra bởi một chuyển trạng thái
- Các hành động bắt nguồn việc chuyển trạng thái
## Thiết kế test case

### All states: **tất cả các trạng thái đều được thăm ít nhất một lần**

### All events: **tất cả các sự kiện đều được kích hoạt ít nhất một lần, có thể bỏ qua trạng thái hoặc các chuyển trạng thái**

### All transitions: **tất cả các chuyển trạng thái được thực hiện ít nhất một lần. Có thể bao gồm all-states và all-events**
- Mạnh: bao phủ hết toàn bộ những cặp chuyển trạng thái có thể có
- Manh hơn nữa: bao phủ hết các cặp 3 trạng thái có thể có

### All paths: **tất cả các đường đều được thực thi ít nhất một lần**





