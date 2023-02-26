Broadcasts là các thành phần tin nhắn, sử dụng để giao tiếp giữa các app với nhau, và cũng với hệt thống Android, khi một sự kiện được quan tâm xảy ra. `Broadcast receiver` là các thành phần trong Android App lắng nghe những sự kiện này và phản hồi phù hợp

Ví dụ, hệt thống Adnroid gửi một sự kiện khi hệ thống được booots lên, khi nguồn diện được kết nối hoặc ngawtsn kết nối, khi headphone được cắm vào hoặc tháo ra. App android cũng có thể thực hiện broadcast các sự kiện, ví dụ khi một dữ liệu mới được tải về

Thông thường, broadcast là các thành phần tin nhắn sử dụng để giao tiếp giữa các app với nhau. Dưới đây có 2 loại broadcast
- `System broadcast` chuyển phát bởi hệ thống
- `Custom broadcast` chuyển phát bởi app

## System broadcast
Là một tin nahwns mà hệ thống Android gửi khi một sự kiện hệ thống xảy ra. Các system broadcast được bọc trong các đối tượng `Intent`. Truowngf hành động của các đối tượng *Intent* chứa chi tiết về sự kiện ví dụ như `android.intent.action.HEADSET_PLUG`,  được gửi đi khi một tai nghe có dây được kết nối hoặc ngắt kết nối. *Intent* có thể chứa thêm các thông tin về sự kiện trong trường `extra`, ví dụ, một `boolean` extra chỉ ra răng tai nghe đã được kết nối hoặc ngắt kết nối

Ví dụ:
- Khi thiết bị được boots, hệ thống sẽ chuyển phát một *system Intent* với hành động là `ACTION_BOOT_COMPLETED`.
- Khi thiết bị bị ngắt kết nối với nguồn điện ngoài, hệ thống gửi một *system Intent* với trường hành động: `ACTION_POWER_DISCONNECTED`

Hệ thống chuyển phát không tập trung vào người nhận cụ thể. Các app có quan tâm phải đăng kí một thành phần để có thể lắng nghe những sự kiện này. Laanhf phần lắng nghe này được gọi là `Broadcast Receiver`

## Custom broadcast
Là một broadcast mà app của bạn có thể gửi đi. Sử dụng custom broadcast khi bạn muốn app của bạn thực hiện các hoạt động mà không phải chạy thêm *Activity*. Ví dụ, sử dụng custom broadcast khi bạn muốn để cho những app khác biết răng dữ liệu đã được downloaded về thiết bị và đã khả dụng để chúng có thể sử dụng. Nhiều hơn một broadcast receiver có thể được đăng kí để nhận broadcast của bạn

Để có thể tạo một custom broadcast, định nghĩa mội *Intent* action 
Có nhiều cách để vận chuyển một custom broadcast:
- Dành cho broadcast thông thường, đẩy intent vào `sendBroadcast()`
- Dành cho broadcast có thứ tự, đẩy một intent tới `sendOrderedBroadcast()`
- Dành cho broadcast local, đẩy intent vào `LocalBroadcastManager.sendBroadcast()`

### Normal broadcast
Phương thức `sendBroadcast()` gửi broadcast tới tất cả các receiver đã đăng kí tại một thời điểm, không có một thứ tự nào cả. Cái này gọi là normal broadcast.Một normal broadcast thưởng là các hiệu quả để gửi broadcast. Với normal broadcast, receiver không thể sinh các kết quả xung quanh chúng, và chúng cũng không thể hủy broadcast

Đoạn code dưới đây gửi một broadcast thường tới tất cả các receiver có quan tâm
```java
public void sendBroadcast() {
	Intent intent = new Intent();
	intent.setAction("com.example.myproject.ACTION_SHOW_TOAST");
	intent.putExtra("data", "This is a normal broadcast");
	sendBroadcast(intent);
}
```

### Broadcast theo thứ tự
Để gửi một broadcast tới từng receiver một, sử dụng `sendOrderedBroadcast()` :
- Thuộc tính `android:priority`  sẽ chỉ ra trong intent-filter quyết định thứ tự khi broadcast được gửi
- Nếu nhiều hơn một recever có cùng thứ tự ưu tiên, nó sẽ gửi theo thứ tự random
- `Intent` được lan truyền từ một receiver tới cái tiếp theo
- Trong suốt lượt của nó, receiver có thể cập nhật *Intent*, hoặc nó có thể hủy broadcast (Nếu như receiver hủy broadcast, *Intent* sẽ không được lan truyền tiếp)
```java
public void sendOrderedBroadcast() {
	Intent intent = new Intent();
	intent.setAction("com.example.myproject.ACTION_NOTIFY");
	sendOrderdBroadcast(intent);
}
```

### Broadcast địa phương
Sử dụng cái này để các *Activity* trong app của mình mới nhận được. Sử dụng phương thức `LocalBroadcastManager.sendBroadcast()`, nó sẽ gửi các broadcast twois các receiver có trong app. Phương thức này hiệu quả, bởi vì nó không tiên quan tới giao tiếp giữa các quá trình. Bên cạnh đó, dùng local broadcast có thể bảo vệ app để chống lại một vài vấn đề về bảo mật

Để gửi một local broadcast:
1. Để lấy instance của `LocalBroadcastManager`, gọ phương thức `getInstance()` và thêm ngữ cảnh của app vào
2. Gọi `sendBroadcast()`, thêm intent mà mình muốn broadcast
```java
LocalBroadcastManager.getInstance(this).sendBroadcast(intent);
```

## Broadcast receiver
Là thành phần ứng dụng có thể đăng kí cho các sự kiện hệ thống và các sự kiện của app. Khi một event xảy ra, các broadcast receiver đã đăng kí sẽ được thông báo qua một *Intent*. Cụ thể, nếu bạn triển khai một app media và bạn quan tâm tới việc biết các lúc người dùng kết nối và ngắt kết nối tai nghe, đăng kí hành động intent `ACTION_HEADSET_PLUG`

Sử dụng broadcast reiceiver để phản hồi lại tin nắn được broadcast từ app của bạn và hệt thống Android. Để tạo một broadcast receiver:
1. Định nghĩa một lớp con của `BroadcastReceiver` và triển khai phương thức `onReceive()`
2. Đăng kí broadcast receiver, tĩnh hoặc động

## Lớp con BroadcastReceiver
Để tạo một broadcast receiver, định nghĩa lớp con của lớp `BroadcastReceiver`. Lớp con này là nơi mà đối tượng *Intent* được gửi đến nếu như intent filter có đăng kí

Bên trong lớp con
- Triển khai phương thức `onReceive()`, được gọi khi `BroadcastReceiver` nhận được *Intent* broadcast
- Bên trong `onReceive()`, bao gồn bất kì logic khác mà broadcast receiver cần

## Ví dụ
```java
private class myReceiver extends BroadcastReceiver {
	@Override
	public void onReceive(Context context, Intent intent) {
		if (intent.getAction().equals(ACTION_SHOW_TOAST)) {
			CharSequence text = "Broadcast Received"	;
			int duration = Toast.NGTH_SHORT;

			Toast toast = Toast.makeText(context, text, duration);
			toast.show();
		}
	}
}
```

Phương thức `onReceive()` được gọi khi app nhận được một *Intent* broadcast đã đăng kí. Phương thức `onReceive()` chạy trong luồng chính, nếu như không có một câu hỏi tưởng minh răng nó phải chạy trên một luồng khác trong `registerReceiver`

Phương thức `onReceive()` có thời gian giớ hạn là 10s. Sau 10s hệ thống android xem xét để khóa receiver lại, và hệ thống có thể hiển thị cho user răng "application not responding". Bởi lý do này, không nên triển khai các hoạt động tốn thời gian ở `onReceive()`

## Đăng kí broadcast receiver và thiết lập intent filter
Có hai loại broadcast receivers:
- Tĩnh, đăng kĩ ở trong AndroidManifest.xml
- Động, đăng kí sử dụng context


### Static
Để đăng kí, bao gồm các thuộc tính sau bên trong thẻ <receiver/> trong file `AndroidManifest.xml`
- `android:name`
Gias trị dành cho thuộc tính này là tên đầy của của lớp con `BroadcastReceiver`, bao gồm cả tên gói. Để sử dụng tên gói chỉ định trong file manifest, đặt trước tên lớp bằng một dấu chấm, ví dụ `.AlarmReceiver`
- `android:exported`
Nếu giá trị được thiết lập là `false`, nhưng app khác sẽ không thể gửi broadcast tới receiver. Thuộc tính này quan trọng trong bảo mật
- `<intent-filter>`
Bao gồm cả thành phần này để chỉ định hành động *Intent* broadcast mà receiver muốn lắng nghe.
```xml
<receiver
	android:name=".AlarmReceiver"
	android:exported="false">
	<intent-filter>
		<action android:name="com.example.myproject.intent.action.ACTION_SHOW_TOAST"/>
	</intent-filter>
</receiver>
```

## Intent filter
Intent filter chỉ định loại intent mà thành phần của bạn có thể nhận. Khi hệ thống nhaaj một *Intent* như là một broadcast, nó tìm kiếm các broadcast receiver dựa trên gái trị chỉ địn trong intent filter của receiver

Để tạo một intent filter tĩnh, sử dụng thẻ <intent-filter/> trong Android manifest. Một phần tử <intent-filter/> có một  thanhf phần yêu cầu, đó là thẻ <action/>. Hệ thống Android so sánh hành động *Intent* tới từ broad cast với hành động ở trên filter. Nếu như trùng tên, broadcast sẽ được gửi tới ứng dụng của bạn.
Intent-filter dưới đây lắng nghẹ broadcast của hệt thống và gửi khi thiết bị được bật lên. Chỉ đối tương *Intent* với hành động có tên là `BOOT_COMPLETED` trùng vời filter:
```xml
<intent-filter>
	<action android:name="android.intent.action.BOOT_COMPLETE"/>
</intent-filter>
```

Nếu không có intent filter nào được chỉ định, broadcast receiver chỉ có thể được kích hoạt với một *Intent tường mình* được chỉ định bởi tên. (Điều này giống như các intent tường minh được sử dụng để chạy các *Activity* bằng tên của chúng)

## Receiver động
Receiver động còn được gọi là `context-registered receiver`. Bạn đăng kí một receiver động sử dụng app contetnxt hoặc một *Activity* context. Một receiver động nhận broadcast miến là ngữ cảnh đăng kí hợp lệ
- Nếu abnj sử dụng application context để đăng kí receiver, ứng dụng của bạn nhận các broadcast thích hợp miễn là app của bạn đang chạy trong foreground hoặc background
- Nếu bạn sử dụng *Activity* context để đăn kí receiver, app của bạn nhận các broadcast thích hợp cho tới khi *Activity* bị hủy
Để sử dụng ngữ cảnh(context) để đăng kí reciever động, làm theo các bước sau:
1. Tạo một *IntentFilter* và thêm *Intent action* mà bạn muốn app lắng nghe. Bạn có thể thêm nhieefuhown một action vào trong cùng một *Intent Filter*
```java
IntentFilter intentFilter = new IntentFilter();
filter.addAction(Intent.ACTION_POWER_CONNECTED);
filter.addAction(Intent.ACTION_POWER_DISCONNECTED);
```

Khi nguồn được kết nối hoặc ngắt keetsnoois, hệ thống *Android* phát các `INTENT.ACTION_POWER_CONNECTED` và `Intent.ACTION_POWER_DISCONNECTED`
2. Đăng kí receiver bằng cách gọi `registerReceiver()` trong context. Truyền đối tượng `BroadcastReceiver` và `IntentFilter`
```java
mReceiver = new AlarmReceiver();
this.registerReceiver(mReceiver, intentFilter);
```

Trong ví dụ trên, ngữ cảnh của *Activity* (this) được sử dungjdder dadwgn kí receiver. Bởi vậy app của bạn sẽ nhận được broadcast cho tới khi nào *Activity* còn hoạt động


## Local broadcast
Bạn phải đăng kí local receiver động, bởi vì đăng kí tĩnh trong file manifest thì không thể được đanh cho local broadcast
Để đăng kí một receiver cho local broadcast:
1. Lấy một instance của `LocalBroadcastManager` bằng cách gọi phương thức `getInstance()`
2. Gọi phương thức `registerReceiver()` , truyền receiver và `IntentFilter` vào
```java
LocalBroadcastManager.getInstance(this).registerReceiver(mReceiver, new IntentFilter(CustomReceiver.ACTION_CUSTOM_BROADCAST));
```

## Hủy đăng kí receiver
Để tiết kiệm tài nguyên hệ thống và hạn chê bị rò rỉ, hủy đăng kí receiver động khi app bạn không còn sử dụng chúng nữa, hoặc là trước khi *Activity* hoặc app bị phá hủy. Điều này luôn đúng dành cho local broadcast receiver, bởi vì chúng được đăng kí động.
Để hủy đăng kí một noramla broadcas receiver
1. Gọi `unregisterReceiver()` và truyền vào trong đó receiver muốn hủy
```java
unregisterReceiver(mReceiver);
```

Để thực hiện huyer local broadcast reciever:
2. Lấy instance của `LocalBroadcastManager`
3. Gọi phương thức `LocalBroadcastManager.unregisterReceiver()` và truyền vào đó đối tượng `BroadcastReceiver`
```java
LocalBroadcastManager.getInstance(this).unregisterReceiver(mReceiver);
```

Bạn muốn hủy khi nào thì phù thuộc vào vòng đời mong muốn của đối tượng `BroadcastReceiver`
	1. Thỉnh thoảng, reciever chỉ cần khi mà hoạt động của bạn được hiển thị, ví dụ như ngắt kết nối mạng khi mạng không khả dụng, Trong trường hợp này, đăng kí receiver trong `onResume()` và hủy nó trong `onPause()`;
5. Bạn có thể sử dụng `onStart()/onStop()` hoặc `onCreate()/onDestroy()`, nếu chúng phù hợp hơn cho trường hợp của bạn

## Hạn chế broadcast
Broadcast không hạn chế có thể gây ra mối đe doạn an ninh, bởi vì  bấy kì reicever nào đăng kí đuề có thể nhận được nó. Ví dụ, nêu snhuw app của ban sử dụng một broadcast normal để gửi một *Intent* không tường minh bao gồm các thông tin nhạy cả, một app khác chưa malware có thể nhận được broadcast. Hạn chế broadcast được khuyên khích mạnh mẽ

Cách để hạn chế một broadcast:
- Nếu có thể, sử dụng `LocalBroadcastManager`, nó sẽ giữ cho dữ liệu bên trong app của bạn, tránh được bất kì vấn đề rò rỉ thông tin. Nếu bạn chỉ có thể dùng *LocalBroadcastManager* nếu bạn không cần phải giao tiếp với những App khác
- Sử dụng phuowng thức `setPakage()` và đẩy vào tên package. Broardcast đươc jhanj chết tới những app mà trùng với tên gói chỉ định
- Bắt buộc quyền truy cập ở phía gửi, hoặc ở phía nhận hoặc cả hai

Để bắt buộc mọt quyền khi gửi broadcast:
- Cung cấp một tam số quyền không null tới `sendBroadcast()`. Chỉ reicever yêu cầu quyền này sử dụng thẻ <uses-permissioni/> trong file *AndroidManifest* mới có thể nhận được broad cast

Để bắt buộc có quyền khi nhận broadcast:
- Nếu bạn đăng kí receiver động, cung cấp một quyền không null tới `registerReceiver()`Ao
- Nếu bạn đăng kí receiver tính, sử dụng thuộc tính `android:permission` bên trong thẻ <receiver/> trong `AndroidManifest`