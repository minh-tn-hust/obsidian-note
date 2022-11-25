## JSX
**JSX = Javascript \- XML**
Chú pháp
```jsx
<JSXElementName JSX_Attributes>

</JSXElementName>
```
Khi biên dịch, JSX chuyển đổi từ cú phát giống XML thành Javascript gốc
	1. Các phần từ XML được chuyển thành các lời gọi hàm
	2. Các thuộc tính XML đượ chuyển đổi thành các đối tượng
Tuân thử theo XML nên cấu trúc khi code có cấu trúc cây phân cấp
Nhúng các biểu thức : { }

---

## React và ReactNative
### React
	- thư viện hỗ trợ xây dựng giao diện ứng dụng, xây dựng các component
	- phát triển hướng thành phần (phân chia giao diện thành nhiều thành phần, kết hợp lại với nhau để tạo ra được giao diện người dùng)
	- component có thể có sẵn hoặc là do người dùng tạo ra

#### Lợi ích
	- Mã nguồn dễ dàng tái sử dụng
	- Khả năng đọc lại mã nguồn tốt hơn
	- Kiểm thử dễ dàng

#### Các khái niệm
- **component** : các các lớp javascript cơ bản, mở rộng từ React.component
	- props : các thuộc tính của component, được truyền vào, và chỉ có thể đọc, không thể ghi đè, component nào cũng có props.child
	- state : các trạng thái của component
- **stateless**: dạng function
- **statefull** : dạng class
- phương thức render : thực hiện xử lý và hiển thị đối tượng lên màn hình

#### Lifecycle
>Component bao gồm nhiều trạng thái, khi chuyển đổi trạng thái sẽ có các phương thức hỗ trợ cho việc chuyển đổi trạng thái

#### VitualDOM
> Sử dụng để kiểm tra xem component nào đã thay đổi trạng thái vầ thực hiện rerender lại component

- Cơ chế hoạt động
	- Khi các component được tạo ra, một Virtual DOM sẽ được thạo ra
	- Khi trạng thái của componet nào đó thay đổi, React sẽ cập nhât Virtual DOM đồng thời vẫn giữ phiên bản Virtual DOM trước để so sánh, điều này giú Virtual DOM tìm ra được component nào thay đổi, khi đó React sẽ chỉ render lại các component đó

## React Native
> Thay vì sử dụng các phần tử HTML, RN cung cấp một số component React có sẵn cho nhà phát tiển và điuề này giúp tạo ra các phần tử Native UI trên nền thảng đích

#### Lifecycleo
- mounted : chứa các phwuogn thức được gọi khi component được khởi tạo và insert vào DOM
- update : chứa các phương thức được gọi khi một component được render lại
- unmouted : chứa các phương thức được gọi khi một component được gỡ bỏ khỏi DOM
