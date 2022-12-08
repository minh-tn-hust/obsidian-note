# Mục tiêu

> Định nghĩa mục đích các phần tử thiết kế + làm rõ vòng đời

> Phân tích sự tương tác của các lớp phần tích và xác định các phần tử mô hình thiết kế

## Mẹo đóng gói
- Nếu có khả năng giao diện hệ thống sẽ trải qua những thya đổi đáng kế
	- Các lớp biên sẽ được đặt trong các package riêng biệt
- Nếu không chác giao diện hệ thống sẽ trải qua những thay đổi đáng kể
	- Các lớp biên sẽ đưcọ đóng gói cùng với các lớp có liên quan với nhau về chức năng

### Các lớp liên quan với nhau về chức năng
#### Tiêu chí xác định các lớp có liên quan đến nhau về mặt chức năng hay không
- Những **thay đổi về hành vi và/hoặc cấu trúc** của một lớp đòi hỏi những thay đổi trong lớp khác
- Loại bỏ một lớp ảnh hưởng đến lớp khác
	- Hai **đối tượng tương tác với số lượng lớn các thông điệp** hoặc có giao tiếp phức tạp
- Một lớp biên có thể liên quan về mặt chức năng với một lớp thực thể củ thể nếu chức năng lớp biên là thể hiện lớp thực thể
- Hai lớp có mối quan hệ với nhau
- Một lớp tạo instance của lớp khác
#### Tiêu chí xác định khi nào không đặt hai lớp trong cùng 1 package
- Không nên đặt hai lớp có liên quan đến các tác nhân khác nhau trong cùng một package
- Một lớp ==tùy chọn== và một ==lớp bắt buộc== nên được đặt trong cùng một package


## Tổng quát về mẫu thiết kế **Hướng đối tượng**
- phần mềm giải quyết đúng các chwucs năng mà user yêu cầu
- phải hạn chế được việc tái thiết kế lại trong tương lại, cho dù vì lý do gì
- bản thiết kế hiện hành phải hỗ trợ tốt nhất việc tái thiết kế lại nếu vì lý do gì đó phải tái thiết kế lại phần mềm
### Phân loại các mẫu thiết kế
#### Structural (nhóm mẫu cấu trúc)
> Các mẫu này cung cấp cơ chế để quản lý cấu trúc và mối quan hệ giữa các class, thí dụ để dùng lại các class có sẵn (class thư viện, class của bên thứ 3) để tạo mối ràng buộc thấp nhất giưa các classs (lower coupling) hay cung cấp các chơ chế thừa kế khác

#### Creational (nhóm mẫu phục vụ khởi tạo đối tượng)
> Giúp khắc phục các vấn đề về khởi tạo đối tượng, nhất là đối tượng lớn và phức tạp, hạn chế sự phục thuộc của phần mềm và platform cấp thấp

#### Behaviral (nhóm hành vi)

