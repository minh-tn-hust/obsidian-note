```
type : project
```

# Ý tưởng
Tạo ra một hệ thống máy chấm thi có khả năng chịu tại từ 500 - 1000 user cùng lúc thực hiện các yêu cầu request tới server. Hệ thống chính gồm 3 phần chính. 

## Phần 1: Hệ thống quản lý

Hệ thống quản lý đảm nhận nhiệm vụ quản lý các cuộc thi và các bài toán được đăng lên hệ thống. Tính năng chính của hệ thống này là quản lý cuộc thi và quản lý bài toán.

## Phần 2: Hệ thống chấm bài

Hệ thống chấm bài là hệ thông ghi nhận bài thi được các thi sinh tham gia gửi lên hệ thống, thực thi các bài thi đó theo một ngôn ngữ lập trình được lựa chọn từ trước và sau đó đối chiếu với các test case đã được các người quản lý đăng lên từ trước và trả về kết quả

## Phần 3: Hệ thống thi

Hệ thống hiển thị các bài toán hiện có trong hệ thống, các cuộc thi. Người dùng có thể thực hiện giải các bài toán hoặc tham gia vào các cuộc thi. Hệ thống hiển thị đề thi và người dùng có thể đính kèm tệp hoặc là nạp nguyên source code

