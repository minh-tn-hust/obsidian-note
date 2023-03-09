# S - Single-responsiblity principle
> Mỗi lớp chỉ có một nhiệm vụ duy nhất. Lưu ý, 1 nhiệm vụ không có nghĩa là một phương thức. Một nhiệm vụ được cài đặt bằng 1 loạt các phương thức trong lớp

Xem xét ví dụ dưới đây
```java
public class Employee {
    private String name;
    private String department;
    private double salary;

    public Employee(String name, String department, double salary) {
        this.name = name;
        this.department = department;
        this.salary = salary;
    }

    public void calculateSalary() {
        if (department.equals("Sales")) {
            salary = salary + (salary * 0.1);
        } else if (department.equals("Marketing")) {
            salary = salary + (salary * 0.15);
        } else if (department.equals("IT")) {
            salary = salary + (salary * 0.2);
        }
        System.out.println("Salary of " + name + " in " + department + " department is " + salary);
    }
}

Ở ví dụ trên, nhìn thoạt qua có vẻ ổn nhưng thực sự không ổn tí nào. Việc để phương thức tính toán lương trong lớp nhân viên thực sự không phù hợp. Nó không liên quan gì tới các thông tin mà lớp Employee đang nắm dữ. Khi thay đổi các tính toán lương, ta phải trực tiêm thay đổi lớp Employee và nó vi phạm nguyên tắc. Thay vào đó nên tạo lớp riêng biệt để tính toán lương và sử dụng lớp này bên trong lớp Employee để đảm bảo nguyên tắc Single-responsiblitiy

```


# O - Open-closed principle
>Nguyên lý này đề cập đến việc một đối tượng phải luôn MỞ cho việc mở rộng, nhưng ĐÓNG trong việc thay đổi
>1. Mở cho việc mở rộng: một module (class) cung cấp các điểm mở rộng, cho phép nó thay đổi hành vi. Một kỹ thuật hay sử dụng là kỹ thuật đa hình, sử dụng các hành vi mở rộng của đối tượng tại thời điểm biên dịch (tùy đối tượng thật sự lúc đó là gì)
>2. Đóng cho việc thay đổi: Không cần/hạn chế tối đa việc thay đổi code, vẫn đảm bảo tính mở rộng như vậy

Ví dụ: 
Xây dựng hệ thống bảo hiểm. Trước tiên cần kiểm tra các giấy tờ người dùng mang tới. Hệ thống sẽ kiểm tra, nếu giấy tờ hợp lệ mới tiền hành xử lý bảo hiểm

Theo nguyên lý một nhiệm vụ, ta tách làm hai lớp. Lớp HealthInsuranceSurveyor có nhiệm vụ xác nhận, và một lớp ClaimApprovalManager có nhiệm vụ xử lý đơn bảo hiểm

```java
class HealthInsuranceSurveyor {
	public boolean isValidClaim() {
		// logic để xác thực giấy chứng nhận chăm sóc sức khỏe
	}
}

class ClaimApprovalManager {
	public void processHealthClaim(HealthInsuranceSurveyor surveyor) {
		if (surveyor.isValidClaim()) {
			// logic kiểm tra giấy chứng nhận
		}
	}

}
```

Nguyên lý trên đã thỏa mãn *Single-responsiblity*, nhưng khi việc kiểm tra logic phải đi kèm với kiểm tra cả bằng lái, khi đó lớp ClaimApprovalManager sẽ phải triển khai thêm phương thức để xử lý cho bằng lái, và phải cung cấp thêm một lớp `VehicleInsuranceSurveyor` 
```java
class HealthInsuranceSurveyor {
	public boolean isValidClaim() {
		// logic để xác thực giấy chứng nhận chăm sóc sức khỏe
	}
}

class VehicleInsuranceSurveyor {
	public boolean isValidClaim() {
		// logic để xác thực giấy chứng nhận chăm sóc sức khỏe
	}
}

class ClaimApprovalManager {
	public void processHealthClaim(HealthInsuranceSurveyor surveyor) {
		if (surveyor.isValidClaim()) {
			// logic kiểm tra giấy chứng nhận
		}
	}

	public void processVehicleClaim(VehicleInsuranceSurveyor surveyor) {
		if (surveyor.isValidClaim()) {
			// logic kiểm tra giấy chứng nhận
		}
	}

}
```

Việc triển khai trên đây đã vi phạm *Open-closed principle* vì khi thêm tính năng mới, ta phải can thiệp vào lớp **ClaimApprovalManager**, thêm code, bla bla rất mất thời gian. Trong khi, thứ mà ta mong muốn là chỉ cần thêm một lớp `VehicleInsuranceSurveyor` và lớp `ClaimApprovalManager` có thể vẫn đáp ứng được. Dưới đây là cách khắc phục, cho dù bạn có thêm bao nhiêu cái giấy chứng nhận đi nữa thì cũng chỉ cần triển khai lớp giấy chứng nhận tương ứng, còn `ClaimApprovalManager` vẫn se thích ứng được. 
```java
interface IInsuranceSurveyor {
	public boolean isValidClaim();
}
class HealthInsuranceSurveyor implements InterfaceSurveyor {
	public boolean isValidClaim() {
		// logic để xác thực giấy chứng nhận chăm sóc sức khỏe
	}
}

class VehicleInsuranceSurveyor implements InterfaceSurveyor {
	public boolean isValidClaim() {
		// logic để xác thực giấy chứng nhận chăm sóc sức khỏe
	}
}

class ClaimApprovalManager {
	public void processClaim(IInsuranceSurveyor surveyor) {
		if (surveyor.isValidClaim()) {
		}
	}
}
```

Việc triển khai như trên đã đảm bảo được 2 principle
- Single-responsiblity: Khi mà việc kiểm tra giấy chứng nhận sẽ do lớp **IInsuranceSurvayor** đảm nhiệm, và các logic về xác thực khác sẽ do lớp **ClaimApprovalManager** đảm nhận
- Open-closed: Khi thêm một loại giấy xác thực mới, ta chỉ cần triển khai loại giấy xác thức đó vào hệ thống bằng các implement từ interface của **IInsuranceSurveyor**, mà không cần quan tâm tới **ClaimApprovalManager** 


# L - Liskov subsitution principle
> Là nguyên lý mà khi lớp con hoàn toàn có thể thay thế được cho lớp cha mà không gặp vấn đề gì. Nếu lớp con thay đổi bản chất hành vi của lớp cha, thì có khả năng sẽ gặp vấn đề

>Ví dụ:
>Nếu một lớp Animal và các lớp con của nó là Dog, Cat, Bird, thì các đối tượng của các lớp con này nên có thể thay thế được cho đối tượng Animal xuất hiện trong hệ thống. Check ví dụ dưới đây về việc vi phạm

Ví dụ 1: Lớp con không thể hoàn thành các hành động của lớp cha
```java
public class Animal {
	public void fly() {
		// do something
	}
}

public class Dog extends Animal {
	// cannot fly
}

Animal animal = new Dog();
animal.fly(); // Việc gọi như thế này sẽ dãnh đến lỗi hoặc các hành vi không mong muốn của lớp dog
```

Ví dụ 2: Lớp con thay đổi luôn hành vi của lớp cha
```java
public class Animal {
	public void makeASound() {
		System.out.print("Some sound is going out");
	}
}

public class Dog {
	@Override
	public void makeASound() {
		System.out.print("Gâu gâu");
	}

}

Animal a = new Dog();
a.makeASound(); // Lúc này ẽ in ra là "Gâu gâu" thay vì là "Some sound is going out"
```

Ví dụ 3:
```java
public class Project {
	public ArrayList<ProjectFile> projectFiles;

	public void loadAllFiles() {
		for (ProjectFile file : projectFiles) {
			file.loadFileData();
		}
	}

	public void saveAllFiles() {
		for (ProjectFile file : projectFiles) {
			file.saveFileData();
		}
	}
}

public class ProjectFile {
	public string filePath;
	public byte[] fileData;
	public void loadFileData() {
	}
	public void saveFileData() {
	}
}

// Triển khai như thế này, thì khi được thay thế vào lớp cha (ProjectFile), thì
// đã thay đổi hành vi của lớp cha, khiến việc thay thế cho lớp cha là không thể
public class ReadOnlyFile extends ProjectFile {
	@Override
	public void saveFileData() throws new InvalidOPException {
		throw new InvalidOPException();
	}
}
```
Dưới đây là cách khắc phụ để hệ thống có thể đáp ứng được 3 principle (dưới đây là 5 nguyên lí được đảm bảo)
```java
interface LoadFile {
	public void loadFileData();
}

interface WriteFile {
	public void saveFileData();
}


public class Project {
	public ArrayList<ProjectFile> projectFiles;

	public void loadAllFiles() {
		for (ProjectFile file : projectFiles) {
			file.loadFileData();
		}
	}

	public void saveAllFiles() {
		for (ProjectFile file : projectFiles) {
			if (file instanceof WritableProjectFile) {
				file.saveFileData();
			}
		}
	}
}

public class ProjectFile implements LoadFile, WriteFile {
	public string filePath;
	public byte[] fileData;
	public void loadFileData() {
	}
	public void saveFileData() {
	}
}

public class WritableProjectFile extends ProjectFile {
	@Override
	public void saveFileData() {
	}
}

public class NonWritableProjectFile extends ProjectFile {
	@Overried
	public void saveFileData() {
	}
}



```
# I - Interface segregation principle - nguyên lý phan tách giao diện
> - Một giao diện không nên chứa các phương thứ mà lớp thực thi không cần đến
> - Một interface đa năng ("Fat interface") nên được chia tách thành các interface nhỏ hơn, có nhiệm vụ cụ thể
> Mục đích của ISP là khuyến khích chia nhỏ các interface, để các lớp cần cái gì thì triển khai cái đấy. Ví dụ, mình có thể tạo ra một interface lớn bao gồm các phương thức `create()` , `read()`, `update()`, `delete()` nhưng một số lớp không cần thiết phải có cả 4 phương thức. Ta nên chia nhỏ interface ra

Xét ví dụ dưới đây:
```java
```

Lớp `NonBreakRobot` không cần thiết phải implement cả 2 phương thức `work()` và `takeBreak()`, điều này đã vi phạm ISP, thay vào đó ta có thể chỉnh sửa lại như sau
```java
interface Toy {
	void setPrice(double price);
	void setColor(String color);
	void move();
	void fly();
}

// Rõ ràng, đối với ngôi nhà đồ chơi, ta không nhất thiết phải thực
// hiện implement các phương thức `move()` va `fly()`
public class ToyHouse implements Toy {
	double price;
	String color;
	@Override
	public void setPrice(double price) {
		this.price = price;
	}

	@Override
	public void setColor(String color) {
		this.color = color;
	}

	@Override
	public void move() {
		// do Nothing
	}

	@Override
	public void fly() {
		// do Nothing
	}
}
```

Sử lại như sau
```java
interface Toy {
	void setColor(String color);
	void setPrice(double price);
}

interface Movable {
	void move();
}

interface Flyable {
	void fly();
}

// Sau đó mình có thể custom được rất nhiều loại đồ chơi từ
// các interface này, không cần phải triển khai nhưng method không cần
// thiết đối với từng loại interface
public class ToyHouse implements Toy {
	String color;
	double price;
	@Override
	public void setColor(String color) {
	}

	@Override
	public void setPirce(double price) {
	}
}

public class ToyCar implements Toy, Movable {
	String color;
	double price;
	@Override
	public void setColor(String color) {
	}

	@Override
	public void setPirce(double price) {
	}

	@Override
	public void move() {
	}
}

public class ToyFly implements Toy, Flyable {
	String color;
	double price;
	@Override
	public void setColor(String color) {
	}

	@Override
	public void setPirce(double price) {
	}

	@Override
	public void fly() {
	}
}

public class ToyPlane implements Toy, Flyable, Movable {
	String color;
	double price;
	@Override
	public void setColor(String color) {
	}

	@Override
	public void setPirce(double price) {
	}

	@Override
	public void fly() {
	}

	@Override
	public void move() {
	}
}

// Đối với việc tạo ra nhiều thứ mà mỗi thứ ghép mảnh từng cái như này
// ta sinh ra một lớp Builder() để thực hiện build các đối tượng theo
// yêu cầu (cái này tương đương với DP Builder)

pulic void ToyBuilder {
	public static ToyHouse buildToyHouse() {
		return new ToyHouse();
	}

	public static ToyCar buildToyCar() {
		return new ToyCar();
	}

	public static ToyPlane buildToyPlane() {
		return new ToyPlane();
	}
}
```




# D - Dependency Inversion Principle
