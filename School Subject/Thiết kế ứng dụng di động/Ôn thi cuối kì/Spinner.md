Cung cấp một cách nahnh chogns để người dugnf lựa chọn một giá trị tỏng một tập. Người dùng tap vào spinner để thấy được danh sách drop-down với tất cả các gái trị có sẵn

Để khởi tạo một spinner, sử dụng lớp *Spinner*, thứ tạo một *View* và hiển thị các giá trị spinner riêng lẻ dưới dạng phần tử View con và cho phép người dùng chọn một.
1. Khởi tạo một phần từ *Spinner* trong XML và chỉ định các gí trị của nó bằng cách sử dụng một mảng hoặc một *ArrayAdapter*
2. Tạo *Spinner* và adapter của nó sử dụng lớp *SpinnerAdapter*
3. Định nghĩa hàm gọi khi lựa chọn dành cho *Spinner*, cập nhật *Activity* có sử dụng *Spinner* để triển khai *AdapterView.OnItemSelectedListenr*

## Tạo Spinner trong file XML
```xml
<Spinner
	android:id="@+id/label_spinner"
	android:layout_width="wrap_content"
	android:layout_height="wrap_content"
/>
```

## Chỉ định các giá trị dành cho Spinner
Thêm một adapter để có thể lấp đầy vào danh sách *Spinner* bằng ccs giá trị. *Adapter* giống như một cái cầu, hoặc là người trung gian, đưungs ở giữa hai giao diện không tương thích. 

*Adapter* lấy tập dữ liệu mà bạn đã chỉ định, tạo một *View* cho mỗi item của dataset

Lớp `SpinnerAdater`, triển khai từ lớp `Adapter`, cho phép bạn định nghĩa 2 loại *View* khác nhau:
- Một cái hiển thị giá trị gữ liệu trong Spinner
- Một cái hiển thị dữ liệu trong danh sách drop-down khi mà *Spinner* được chạm vào

Các giá trị cung cấp cho *Spinner* có thể đến từ bất kì nguồn nào, nhưng phải được cung cấp thông qua một *SpinnerAdapter*, ví dụ như một `ArrayAdapter` nếu như giá trị có thể dễ dàng lưu trong một mảng. 

## Triển khai interface *OnItemSelectedListener* trong Activity
Định nghĩa phương thức lựa chọn dành cho Spinner, cập nhật *Activity* có sử dụng *Spinner* để triển khai interface `AdapterView.OnItemSelectedListener`

## Tạo Spinner và Adapter của nó
Vị trí tốt nhất để tạo Spiner và set các listener của nó  là sau khi *Activity* được infalted trong phương thức `onCreate()`
1. Khởi tạo một instance cuar *Spinner* trong phương thức `onCraete()` và cài đặt listener cho nó bên trong phương thức `onCreate()`
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
	Spinner spinner = findViewById(R.id.label_spinner);
	if (spinner != null) {
		spinner.setOnItemSelectedListener(this);
	}
}
```

2. Tiếp tục chỉnh sửa phương thức `onCreate()`, thêm câu lệnh để tạo `ArrayAdapter` với mảng xâu sử dụng nguồn Android layout cho mỗi item
```java
ArrayAdapter<CharSequence> adapter = ArrayAdapter.createFromResource(
										this, 
										R.array.labels_array, 
										android.R.layout.simple_spinner_item);
```

3. Chỉ định layout cho *Spinner* lúc được chọn là `simple_spinner_dropdown_item`, và áp dụng adapter cho *Spinner*
```java
adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
if (spinner != null) {
	spinner.setAdapter(adapter);
}
```

4. Thêm code để phản hồi khi *Spinner* được lwuaj chọn
```java
public void onItemSelected(AdapterView<?> adapterView, View view, int pos, long id) {
	String spinner_item = adapterView.getItemAtPosition(pos).toString();
}
```

Các tham số của `onItemSelected`
- view:  View mà người dùng lựa chọn trong spinner
- pos: Vị trí của View trong danh sách drop-down
- id: Id hàng của item được lựa chọn