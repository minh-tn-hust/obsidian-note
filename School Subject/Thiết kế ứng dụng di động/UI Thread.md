Khi Android app bắt đầu, nó khởi tạo một luồng chính, gọi là luông UI. Luồng UI bắn ra các sự kiện tới các UI widget riêng biệt. Luồng UI là nơi mà app tương tác với các thành phần từ UI toolkit

Luồng UI cần được chú ý để vẽ UI và giữ cho app phản hồi lại các tương tác của người dùng. Nếu như luồng này bị chậm bởi các thao tác dài như truy cập màng / truy vấn dữ liệu thì có thể làm đơ, block luôn cả UI. 

Để đảm bảo app không block luồng UI
- Hoàn thành tất cả các công việc ít hơn 16ms cho mỗi UI
- Không chạy các task bất đồng bộ hoặc các task dài trên luồng UI. Thay vào đó, triển khai tasks trong luồng background sử dụng *AsyncTassk* hoặc là *AsycTsakLoader * (dành cho các task có độ ưu tiên cao, hoạc là cần phải báo cáo lại cho người dùng hoặc UI)

Đừng sử dụng luồng background để điều khiểu UI bởi vì không an toàn