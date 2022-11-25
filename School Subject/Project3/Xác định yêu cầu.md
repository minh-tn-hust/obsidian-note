# Yêu cầu chức năng
1. **Hệ thống quản lý**
	1.1. Phân quyền chức năng (đăng nhập, đăng xuất)
	1.2. Người quản lý có thể đăng bài kèm theo các test case và các yêu cầu liên quan tới tài nguyên
	1.3. Người quản lý có thể thêm người khác và cấp quyền liên quan
	1.4. Người quản lý có thể tạo các kì thi
	1.4.1. Người quản lý thiết lập quyền người dùng nhìn thấy các kì thi
	1.4.2. Quản lý các **kì thi** được phân quyền từ người tạo cuộc thi
	1.4.3. Có thể chỉnh sửa các thông tin liên quan trong quá trình **kì thi** đang được thực hiện
	1.4.4. Đối với **kì thi** private, người quản lý có khả năng thêm người tham dự vào **kì thi**
	1.4.5. Tính giờ đếm ngược trong các kì thi

2. **Hệ thống chấm thi**
	2.1. Ghi nhận bài thi từ người dự thi và thực thi bài thi
	2.2. Hệ thống phân bố tài nguyên cho các lần thực thi phù hợp
	2.3. Hệ thống thực thi được nhiều ngôn ngữ lập trình
	2.4. Hệ thống tính thời gian thực thi, bộ nhớ chiếm dụng của các bài nạp
	2.5. Có bảng rank cập nhật theo thời gian đối với các **kì thi**
	2.6. Hệ thống thực hiện validate kết quả sau khi đã thực thi các bài thi

3. **Hệ thống làm bài thi**
	3.1. Hiển thị các kì thi hiện đang có, đối với kì thi nào tham gia sẽ hiển thị khác màu
	3.2. Hiển thị danh sách các bài đang available mà người dùng có thể làm
	3.4. Hiển thị các bài đã được giải, các bài chưa làm, các bài đã làm nhưng chưa giải được bằng các màu sắc khác nhau
	3.5. Người dùng có thể xem lại được các bài nạp của mình tới một bài toán
	3.6. Cho phép người dùng nạp file (preview) hoặc copy source code
---
# Yêu cầu phi chức năng
1. **Hệ thống quản lý**
	1.1. Hỗ trợ nhập markdown đối với hệ thống đề bài, có hỗ trợ nhập công thức
2. **Hệ thống chấm thi**
	2.1. Hệ thống có thể đảm bảo tính an toàn khi thực thi các file code từ người dùng gửi lên
	2.2. Hệ thống bảng rank có thể cập nhật realtime hoặc gần realtime
	2.3. Khả năng chịu tải của hệ thống phải đạt được mức từ 500 - 1000 người cùng dự thi một kì thi (đối với đồ án tốt nghiệp, nâng mức lên từ 50.000 - 100.000)
	2.4. Có khả năng hoạt động độc lập trên nhiều máy chủ khác nhau
3. **Hệ thống làm bài thi**
	3.1. Hệ thống có giao diện dễ tương tác, dễ dàng sử dụng
	3.2. Hệ thống kiểm tra nếu như source code nạp lên không có thay đổi so với source code cũ
---
# Biểu đồ usecase
## Biểu đồ usecase tổng quan
![[Usecase tổng quan.png]]
## Biểu đồ usecase quản lý kỳ thi
![[Quản lý kì thi.png]]
## Biểu đồ usecase quản lý bài thi
![[Pasted image 20221124145836.png]]

---
# Luồng kịch bản
## Người quản lý
### Quản lý bài thi
#### Chỉnh sửa test case
#### Chỉnh sửa đề thi
#### Thiết lập yêu cầu hệ thống chấm
#### Xóa đề thi
#### Đăng bài thi
#### Đăng test case

### Quản lý kì thi
#### Chỉnh sửa kì thi
#### Thêm người quản lý vào kì thi
#### Tạo kì thi
#### Thêm bài thi vào kì thi

## Người dự thi
#### Xem danh sách lịch sử nạp bài
#### Làm bài thi
#### Xem danh sách kì thi
#### Xem lịch sử nạp bài

---

# Quy trình hoạt động

## Quy trình đăng nhập, đăng xuất

## Quy trình quản lý tài khoản

## Quy trình quản lý kì thi

## Quy trình đăng bài

## Quy trình tham gia kì thi

## Quy trình tham gia giải bài

## Quy trình chấm bài
# Biểu đồ usecase
---
# Biểu đồ sequence

---
# Biểu đồ giao tiếp
---


# Biểu đồ lớp phân tích
---
# Biểu đồ lớp thiết kế
---


