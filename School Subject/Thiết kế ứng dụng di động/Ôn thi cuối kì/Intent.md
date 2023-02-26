Mỗi haotj động được bắt đầu / kích hoạt với một *Intent*, là một  message object tạo yêu cầu tới *Android runtime* để bắt đầu một *Activity* hoặc thành phần khác trong app hoặt ở một app khác

## Note 1
Intent có thể pass data qua lại giữa các *Activity*

## Các loại intent
- Tương minh: Bạn chỉ định hoạt động nhận (hoặc thành phần khác) sử dụng tên của class. Sử dụng *Intent tường minh* để bắt đầu thành phần có trong app
- Không tường minh: Bạn không chỉ *Activity* cụ thể nào haotj thành phần nào nhận *intent*. Thay vào đó, bạn định nghĩa một hành động chung để thực hiện, và hệ thống Android sẽ kết nối request của bạn tới một *Activity* hoạt các thnahf phần khác mà có thể xử lý được hành động được request. 

## Intent object và các trường
Đối với *Intent tường minh*, các trường chính bao gồm:
- *Acitivity class* : Đây là class name của Acitivity hoạt những thành phần khác mà có thể nhận *Intent*. Ví dụ như *com.example.SampleActivity.class*. Sử dụng *Intent constructor* hoặc là các phương thức *setComponent()*, *setComponentName()*, hoặc là *setClassName()* để chỉ định class
- *Intent data*: Là trường chứa một thể hiện tới dữ liệu bạn muốn *Acitivity nhận* để xử xử lý như là một *Uri Object*

- *Intent extra*: Đây là những cặp khóa-giá trị mà mang thông tin *Activity nhận* yêu cầu để hoàn thành hành động được yêu cầu
- *Intent flags*:  Những bit thêm vào, định nghĩa lopws *Intent*. Những trường này chỉ định cho hệ thống Android cách để chạy *Activity* hoạt cách để đối xử với nó sau khi được khởi chạy

## Bắt đàu một *Activity* với một *Intent tường minh*

Để bắt đầu  một *Activity* cụ thể từ một *Activity* khác, sử dụng *Intent tường mình* và phương thức *startActivity()*. Xem ví dụ sau
```java
Intent mesageIntent = new Intent(this, ShowMessageAcitivity.class);
startActivity(messageIntent);
```

Intent constructor sử dụng 2 tham số dành cho một *Intent tường minh*
- Một App context. Trong ví dụ này, lớp *Activity* cung cấp *content* - ngữ cảnh
- Thành phần cụ thể để bắt đầu (*ShowMessageActivity*) 

Có thể tắt thủ công *Activity* được bắt đầu trong phản hồi lại hành động người dùng với phương thức `finish()`
```java
public void closeActivity(View view) {
	finish();
}
```

## Truyền dữ liệu từ một *Acitivity* tới một cái khác
Ngoài việc để bắt đầu một Acitivity từ một caics khác, sử dụng *Intent* để truyền thông tin từ *Activity* này tới *Activity* khác. *Intent object* bạn sử dụng để bắt đầu *Acitivty* có thể bao gồm *Intent data* (URI của một đối tượng để hành động) hoặc là sử dụng *Intent extras*.
### Flow thực hiện gửi và nhận data giữa các Intent
Đối với Acitivity gửi:
1. Tạo một *Intent object*
2. Đẩy data hoặc là extras vào trong *Intent*
3. Bắt đầu một *Activity* với `startActivity()`

Đối với *Activity* nhận
1. Lấy *Intent object* từ *Activity* được bắt đầu cùng
2. Phục hồi lại data/extras từ *Intent object*

```java
class SendActivity() {
	public static void handleSendIntentWithData() {
		Intent messageIntent = new Intent(this, ShowMessageActivity.class);
		messageIntent.setData(Uri.parse("http://www.gooogle.com"))
		startActivity(messageIntent);
	}

	public static void handleSendIntentWithExtras() {
		Intent messageIntent = new Intent(this, ShowMessageActivity.class);
		messageIntent.putExtra(EXTRA_MESSAGE, "THIS IS MESSAGE");
		startActivity(messageIntent);
	}
}

class ReceiveActivity() {
	public static void handleReceiveIntent() {
		Intent intent = getIntent();
		Uri locationUri = intent.getData(); // lấy thông tin từ trường data
		// lấy thông tin từ trường Extra
		String message = intent.getStringExtra(EXTRA_MESSAGE);
		int positionX = intent.getIntExtra(EXTRA_POSITION);

		// lấy luôn cả extras Bundle
		Bundle extras = intent.getExtras();
		String message = extras.getString(EXTRA_MESSAGE);
	}
}
```

## Truyền dữ liệu ngược lại *Activity*
Khi bắt đầu một hoạt động với một *Intent*, *Activity* khởi nguồn sẽ được tạm dừng, cho tới khi *Activity* được bắt đầu mới kết thúc bằng việc người dùng nhấn nút *Back* hoặc là gọi phương thức `finish()`

Thỉnh thoản, sẽ cần phải gửi data ngược trở lại *Activity khởi nguồn*. Để làm được điều đó, chúng ta sẽ cần theo các bước sau
1. Thay vi khởi chạy *Acitivity* bằng phương thức `startActivity()`, gọi phương thức `startActivityForResult()` với *Intent* và một *request code*
2. Khởi tạo một *Intent* mới trong *Acitivity* được khởi chạy và thêm dữ liệu vào *Intent* đó
3. Triển khai phương thức *onActivityResult()* trong *Activity khởi nguồn* để xử lý data được trả về
```java
class SendActivity {
	public static void handleLaunchAcitivyByIntent() {
		Intent intent = new Intent(this, ReceiveAcitity.class);
		startAcitivityForResult(intent, TEXT_REQUEST);
	}
	public void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		if (requestCode == TEXT_REQUEST) {
			if (resultCode == RESULT_OK) {
				String reply = data.getStringExtra(EXTRA_RETURN_MESSAGE);
			}
		}
	}

}

class ReceiveActivity {
	public static void handleCloseActivityWithReturnData() {
		Intent returnIntent = new Intent();
		returnIntent.putExtra(EXTRA_RETURN_MESSAGE, mMessage);
		setResult(RESULT_OK, replyIntent);
	}

}
```


## Di chuyển qua lại giữa các Activity
