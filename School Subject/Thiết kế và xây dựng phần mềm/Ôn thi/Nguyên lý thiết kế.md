# GRASP
>- Nguyên lý/ mẫu thiết kế phần mềm phân định trách nhiệm
>- Hướng tới trọng tâm là phân trách nhiệm cho ai
>Có 9 nguyên lý sử dụng trong GRASP
>	- Information expert
>	- Creator
>	- Controller
>	- Low coupling
>	- High cohesion
>	- Indirection
>	- Polymorphism
>	- Pure fabrication
>	- Protected variations


## Information expert: Chuyên gia thông tin
>Trao nhiệm vụ cho lớp có đầy đủ thông tin để hoàn thành nhiệm vụ đó.
>Lớp đó có thể có sẵn các thông tin để trả lời hoặc là lớp có thể giao tiếp và trao đỏi với các lớp khác để láy đủ thông tin cần thiết cho việc thực hiện nhiệm vụ

### Ví dụ:
Lấy tất cả các videos trong *VideoStore*, vì lớp *VideoStore* có tất cả thông tin về videos, nên việc lấy tât cả các videos trong VideoStore được giao cho lớp VideoStore

## Creator : Khởi tạo
>Ai sẽ chịu trách nhiệm khởi tạo một đối tượng?. Các quyết định sẽ dựa trên quan hệ và tương tác giữa các đối tượng với nhau. Sử dụng để xem xét xem một lớp có thể được khởi tạo từ lớp nào, chứ không phải để áp dụng

## Controller : Điều khiển
>Đối tượng nào sẽ chịu trách nhiệm chuyển request từ các đối tượng UI đến các đối tượng nghiệp vụ.
>Ví dụ: Khi xử lý các thao tác với thành phần UI, các tương tác sẽ gọi tới một lớp Controller để thực hiện xử lý các thao tác nghiệp vụ bên dưới

### Bloated Controller : Điều khiển quá tả
- Lớp Controller quá tải nế:
	- Chịu quá nhiều trách nhiệm
	- Điều khiển, xử lý quá nhiều nhiệm vụ, thay vì chuyển nhiệm vụ cho các lớp khác

## Low Coupling
- Mức độ phụ thuộc vào các đối tượng khác
- Khi một đối tượng thay đổi, sẽ ảnh hưởng đến các lớp phụ thuộc khác
- **Low Coupling** giúp
	- Giảm tác động của sự thay đổi
	- Phân công trác hiệm để đảm bảo kết nối lỏng lẻo
	- Giảo thiểu sự phụ thuộc, hệ thống dễ bảo trì và dễ tái sử dụng mã nguyển

### Hai lớp là phụ thuộc nếu như
- Lớp này liên kết với lớp khác
- Lớp này sử dụng các phương thức của lớp khác
- Lớp này kế thừa lớp khác 

## High Cohesion
>Mức độ liên quan giữa các hoạt động trong một lớp, các hoạt động phải liên quan tới nhau. Víu dụ dưới đây là việc low cohension
```java
class Student {
	public void getStudentDetails(); // -> Hoạt động liên quan tới sinh viên
	public void accessDB(); // -> Hoạt động lien quan tới DB
	public void DBcalls(); // -> Hoạt động liên quan tới DB
	public void insertDB(); // -> Hoạt động liên quan tới DB
}
```

Trên đây, các hoạt động bên trong lớp Student không có liên quan tới nhau, dẫn tới Low Cohesion, việc tách riêng các hoạt động sẽ làm tăng Cohesion
```java
class Student {
	private DBController controller;
	public void getStudentDetails();
}

class DBController {
	public void accessDB();
	public void DBcalls();
	public void insertDB(data);
}
```

Việc tách riêng hai lớp trên làm Cohesioon tăng nhưng nó không đảm bảo cho việc Low Coupling bởi vì trong lớp Student còn phải phụ thuộc vào lớp DBController để thực hiện thao tác truy cập cơ sở dữ liệu. Để có thể đảm bảo luôn cả tính Low Coupling, có thể áp dụng thêm Dependency Injection 

## Gián tiếp - Indirection
>Cách thức phụ thuộc trực tiếp giữa các phần tử
>Indirection sẽ đưa ra một đơn vị trung gian để thực hiện giao tiếp giữa các phần tử, do đó các phần tử không bị trực tiếp phụ thuộc vào nhau, việc này giúp giảm **Coupling**
>Indirection hỗ trợ low coupling nhưng nó lại làm giảm khả năng đọc hiểu code. Bởi vì bạn sẽ không biết được lớp nào đảm nhận việc xử lý các mệnh lệnh từ Controller. Việc này sẽ là sự đánh đổi 

Ví dụ: Sử dụng DI

## Đa hình - Polymorphism
Xử lý các hàn vi khác nhau tùy theo kiểu cụ thể của đối tượng phải làm thế nào???
Sử dụng Đa hình (Xem lại trong OOP)

## Pure Fabrication
Xử lý vấn đề phần trách nhiệm cho lớp nào, khi mà áp dụng các nguyên lý ở trên dẫn tới vi phạm nguyên lý high cohesion và low coupling???

Sử dụng một lớp riêng, tách biệt và gán các nhiệm vụ không liên quan trực tiếp với các đối tượng chính có trong hệ thống cho lớp đó, để giảm bớt sự phức tạp của các lớp và sự phụ thuộc trong hệ thống

Ví dụ: Trong hệ thống quản lý đơn hàng, thay việc các lớp quản lý đơn hàng hoặc khách hàng phải triển khai chức năng gửi email đến khách hàng, ta có thể tách riêng chức năng này ra và cho một lớp giả lập (Service) để các lớp khác có thể thực hiện truy cập vào lớp Service và thực hiện chức năng gửi email

```java
public class EmailSender {
    public static void sendEmail(String email, String message) {
        // code to send email
    }
}

public class Order {
    private String customerEmail;
    private List<Item> items;

    public void checkout() {
        // code to process order
        EmailSender.sendEmail(customerEmail, "Your order has been processed.");
    }
}
```


## Protected Variation 
>Đây là nguyên tắc khuyển khích việc thiết kế các đối tượng để chịu đựng được sự thay đổi và có khả năng thích nghi với các yêu cầu mới mà không ảnh hưởng đến các đối tượng khác trong hệ thống


## Nguyên lý tri thức tối thiểu
Đừng nói chuyện với người lạ thông qua người trung gian, chỉ nên nói chuyện với người trung gian. Dưới đây là trường hợp vi phạm:
```java
class A {
	public void doSomething() {
		B = this.getInterface().getSomething().getB(); // <--- Vi phạm nguyên lý tri thức tối thiểu
	}
}
```

- Trong phương thức M của đối tượng O chỉ được gọi các phương thức của các loại đối tượng sau:
	- Chính đối tượng O
	- Các đối tượng trong tham số của M
	- Các đối tượng được tạo/khởi tạo trong M
	- Các đối tượng thuộc tính của O

```java
class Store {
	public void doAPayment() {
		payment = 2.00; // “I want my two dollars!”
		// Đoạn code này vi phạm nguyên lý tri thức tối thiểu, vì lớp Store
		// thực hiện thao tác trực tiếp với ví của khách hàng (trong thực tế không
		// có chuyện như vậy)
		Wallet theWallet = myCustomer.getWallet();
		if (theWallet.getTotalMoney() > payment) {
				theWallet.subtractMoney(payment);
		} else {
				// come back later and get my money
		}
	}
}
```

Sửa lại 
```java
class Customer {
	private Wallet myWallet;
	public void doAPayment(int money) {
		this.myWallet.lose(money);
	}
}

class Store {
	public void doAPayment() {
		int payment = 2.00;
		Customer customer = this.getCustomer();
		customer.doAPayment(payment);
	}
}
```




















