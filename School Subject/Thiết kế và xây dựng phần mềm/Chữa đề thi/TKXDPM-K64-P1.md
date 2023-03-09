## Câu 2(1):
```java
class A {
	public B b1;
	public void doSomething() {
		this.b1 = new B();	
	}

	public void X(B b2) {
		boolean flag = this.m2(b2);
		if (flag == false) {
			b2.m3();
			return;
		}
		this.b1.m4();
	}


	public boolean m2(B b2) {
		
	}
}

class B {
	public A a;
	public B b;
	public B(){};
	public int m1(A a) {
		b2 = new B();
		a.X(b2);
		this.m4();
		b2.m5();
	}

}

class C {
	public m5(){
	}
}
```



## Câu 3
#### Vi phạm Single-responsiblity
Low Cohension do một lớp đảm nhiều quá nhiều nhiệm vụ, các nhiệm vụ thường không liên quan tới nhau, Low Coupling do một lớp nhận nhiều nhiệm vụ, nên khi nhiệm vụ đó thay đổi, khiến cho các lớp liên quan tới lớp đó cũng phải thay đổi theo

- Phân chia chức năng của một lớp ra thành các lớp nhỏ hơn để đảm bảo rằng mỗi lớp chỉ đảm nhận một trách nhiệm cụ thể.

- Sử dụng kỹ thuật Dependency Injection để tách biệt việc xử lý dữ liệu và hiển thị giao diện, giúp cho các lớp đảm nhiệm một nhiệm vụ cụ thể, tránh việc xử lý quá nhiều chức năng trong cùng một lớp.

- Sử dụng các Design Pattern như Strategy Pattern để đảm bảo rằng phần logic được phân tách riêng rẽ với các phần khác trong lớp, giúp cho mã nguồn dễ dàng bảo trì và mở rộng.

- Sử dụng các kiến trúc mẫu (architecture patterns) như Model-View-Controller (MVC) để phân tách các thành phần của ứng dụng, đảm bảo rằng mỗi lớp chỉ đảm nhận một trách nhiệm duy nhất và giữ cho mã nguồn dễ dàng bảo trì.

#### Open-Close
Cohension : Việc các tính năng mới thêm vào không thể phù hợp được với các chức năng đã chạy của lớp, gây giảm tính cohension của lớp
Coupling: khi thêm mới tính năng, ngoài việc implement tính năng mới được thêm vào class, mình bắt buộc phải kiểm tra xem tính năng được thêm mới vào có thực sự hoạt động đối với các lớp liên quan hay không, việc này gây tăng Coupling

- Sử dụng Interface: Tạo ra các interface để định nghĩa các hành vi, và các lớp cụ thể có thể triển khai các interface này mà không phải sửa đổi mã nguồn của interface. Điều này giúp cho việc mở rộng hệ thống trở nên dễ dàng hơn.

- Sử dụng Abstract Class: Tạo ra các abstract class để định nghĩa một phần hoặc toàn bộ chức năng của một đối tượng. Việc sử dụng abstract class giúp cho các lớp con có thể mở rộng và thêm chức năng mà không phải sửa đổi mã nguồn của abstract class.

- Sử dụng Design Pattern: Sử dụng các Design Pattern như Strategy, Template Method, Factory Method,... để giúp cho việc mở rộng và thêm chức năng trở nên dễ dàng hơn.

- Sử dụng Dependency Injection: Sử dụng Dependency Injection giúp cho việc mở rộng và thêm chức năng trở nên dễ dàng hơn bằng cách tách các phần chức năng và cấu trúc hệ thống thành các module độc lập, và sau đó sử dụng Dependency Injection để kết nối các module này với nhau.


#### Liskov Substitution
Cohension : giảm vì khi các lớp con kế thừa, không thể thực hiện theo định nghĩa của lớp cha mà bắt buộc các lớp con phải tự định nghĩa lại theo hành động của từng lớp con, gây giảm cohension
Coupling : tăng vì khi một lớp con không thể thực hiện thay thế cho một lớp cha, có thể ảnh hưởng tới toàn bộ hệ thống (ví dụ như thay nhầm lớp con cho lớp cha)

Để khắc phục sự vi phạm LSP trong SOLID, ta có thể sử dụng các kĩ thuật trong OOP như:

- Thực hiện việc thiết kế lớp cha sao cho không đưa ra những ràng buộc quá chặt chẽ đối với các lớp con. Tránh sử dụng các điều kiện hay phân nhánh để kiểm tra lớp con.

- Sử dụng Interface và Abstract Class để giảm sự phụ thuộc giữa các lớp. Nếu muốn sử dụng các phương thức khác nhau đối với các lớp con thì ta nên sử dụng Interface hoặc Abstract Class để tạo ra các phương thức trừu tượng, từ đó các lớp con có thể triển khai lại theo ý muốn.

- Sử dụng Polymorphism để giải quyết vấn đề của LSP. Polymorphism cho phép chúng ta triển khai các phương thức có cùng tên trong lớp cha và lớp con, nhưng với cách hoạt động khác nhau. Điều này giúp đảm bảo tính đúng đắn của các hành vi và kết quả của chúng.

- Sử dụng Design Pattern, chẳng hạn như Factory Method Pattern hoặc Abstract Factory Pattern, để tạo ra các đối tượng một cách linh hoạt và tránh vi phạm LSP. Pattern giúp ta tạo ra các đối tượng một cách trừu tượng và linh hoạt, cho phép ta thay đổi hành vi của đối tượng một cách dễ dàng mà không ảnh hưởng đến hệ thống.

#### Interface Segregation

- Tách interface thành các interface con: Thay vì sử dụng một interface lớn chứa nhiều method, chúng ta có thể tách interface thành các interface con nhỏ hơn, với mỗi interface chỉ chứa các method cần thiết cho từng chức năng cụ thể. Ví dụ, nếu một interface có chứa nhiều method, trong đó một số method không được sử dụng cho một số lớp, ta có thể tách nó thành các interface con khác nhau để phù hợp với từng lớp riêng biệt.

- Sử dụng Adapter Pattern: Chúng ta có thể sử dụng Adapter Pattern để tạo ra một interface mới, chứa chỉ những method cần thiết cho một lớp cụ thể. Interface này sẽ thừa kế từ các interface cũ, nhưng chỉ chứa các method cần thiết cho lớp đó. Điều này sẽ giúp tránh việc lớp phải triển khai các method không cần thiết và phù hợp với nguyên tắc Interface Segregation.

#### Dependency Inversion
Để khắc phục vi phạm Dependency Inversion trong SOLID, chúng ta có thể sử dụng các kĩ thuật sau:

- Dependency Injection (DI): Đây là kỹ thuật phổ biến nhất để giải quyết vấn đề về Dependency Inversion. DI giúp chúng ta đưa các phụ thuộc vào trong một đối tượng khác và đưa chúng vào đối tượng cần sử dụng thông qua constructor, setter hoặc interface. Ví dụ:

- Inversion of Control (IoC): Kỹ thuật này giúp chúng ta giảm sự phụ thuộc giữa các lớp và đảo ngược quyền kiểm soát (control) của các đối tượng. Các framework như Spring hay Guice cung cấp chức năng IoC container để quản lý các phụ thuộc và giúp ta giảm sự phụ thuộc. Ví dụ:
- Factory Method Pattern: Kỹ thuật này giúp tách rời việc khởi tạo đối tượng và tạo ra một đối tượng con cụ thể. Factory Method Pattern sử dụng một interface hoặc lớp trừu tượng để tạo ra các đối tượng cụ thể, giúp chúng ta giảm sự phụ thuộc vào các đối tượng cụ thể.


## Câu 4
a. Đầu tiên vi phạm Single-responsiblity, công việc xếp loại Customer thuộc loại nào không nên do lớp Customer đảm nhiệm. Việc thay đổi các xếp Customer sẽ khiên cho phải thay đổi lớp Customer, lớp này chỉ nên lưu trữ các thông tin liên quan tới Customer

Tương tự việc tính discount

Về mức độ couping,  khi mà lớp không phụ thuộc vào lớp nào khác, low coupling
Về cohesion, trong lớp thực hiện nhiều nhiệm vụ dẫn tới low cohesion

b. 



