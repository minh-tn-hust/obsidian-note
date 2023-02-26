Hiện tại Module này đang thực hiện quá nhiều công việc
- Handle gói tin trả về từ server, gửi các gói tin đi (phần này liên quan tới các chức năng về mạng)
- Handle show các màn hình cần thiết
- Xử lý logic liên quan tới model event của người chơi
- Xử lý logic với Model và gọi các UI tương ứng thực hiện Anim


#  Mục đích của cách cấu tạo mơi
> Chia nhỏ TreasureMineModule thành các module nhỏ hơn, cho phép dễ dàng có thể thực hiện test với Cheat. Cung cấp các thông tin rõ ràng hơn về các Module, chia các Module quản lý từng phần riêng của người chơi
## Vấn đề gặp phải
Các module sau khi chia nhỏ lại tương tác với nhau, khiến cho việc code có xử lý logic sử dụng có thể từ 2 -> 3 module gọi nhau liên tiếp

Giải quyết: Sử dụng Mediator Pattern
