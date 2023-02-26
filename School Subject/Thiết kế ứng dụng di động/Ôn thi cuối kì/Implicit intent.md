# Resource
[Intent Document](https://developer.android.com/reference/android/content/Intent)




# Content
Không cần chỉ định chính xác hoạt động (hoặc là thành phần) để chạy thay vào đó, chỉ cần bao gồm đầy đủ thông tin trong *Intent* về *Task* mà bạn muốn khởi chạy. Hệ thống Android sẽ kết nối thông tin có trong *Intent* được request với bất kì hoạt động có sẵn trên thiết bị mà có thể chạy được *Task* đó. Nếu chỉ có một *activity* được kết nối, activity đó sẽ được chạy. Nếu có nhiều acitivity phù hợp với *Intent*, người dùng sẽ được hiển thị một ứng dụng chọn và chọn app nào để thực hiện task

![[Pasted image 20230223122445.png]]

Một *Activity* đăng kí chính nó với hệ thống là có khả năng có thể xử lý được *implicit intent* với *Intent filter*. *Intent filter* là các để hệ thống Android biết được bắt đầu cuj thể *Activity*Anaof trong App khi mà người dùng tab vào icon trên home screen

## Intent actions, categories, và data
Là một instace của lớp *Intent*, giống như *Intent tường mình* nhưng có thêm một vài trường:
- *Intent* action: là chủng acition mà *Activity nhận* nên hành động. Các *Intent action* được định nghĩa như là hằng số trong *Intent class* và bắt đầu bằng từ *ACTION*, thêm vào *Intent* bằng phương thức `setAction()`
- *Intent* category: cung cấp thông tin thêm về tập các component nên xử lý *Intent*. Cái này là tùy chọn, có thể thêm nhiều hơn 1 loại vào *Intent*. Là các hằng số bắt đầu bằng `CATEGORY_`. Thêm vào *Intent* bằng phương thức `addCategory()`
- *Data type* : chỉ ra lại dữ liệu mà *Activity* nên thao tác trên đó. THông thường, data type chỉ định từ URI trong trường data field, nhưng chúng ta có thể định nghĩa nó với phương thức `setType()` // Đoạn này đọc méo hiểu gì cả

## Gửi một implicit Intent
Bắt đầu một *Activity* với một implicit Intent và passing data từ một *Activity* khác, gần như giống như làm với explicit Intent
1. Tạo một *Intent* object
2. Thêm thống tin về yêu cầu vào *Intent* object (thêm action và category hoặc cả hai vào)
3. Gửi *Intent* với `startActivity()`
4. Hiển thị app lựa chọn dành cho request

### Khởi tạo Intent object
```java
Intent sendIntent = new Intent();

// hoặc là khởi tạo với action chỉ định
Itent sendIntent = new Intent(Intent.ACTION_VIEW);

// hoặc là thêm các thông tin bằng các hàm set
Intent sendIntent = new Intent();
sendIntent.setAction(Intent.ACTION_SEND);
sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
sendIntent.setType("text/plain");
```

### Xử lý *Activity* trước khi bắt đầu sử dụng
Khi định nghĩa một *implicit Intent* với hành động hoặc là category được chỉ định, sẽ có khả năng là không có *Activity* nào trên thiết bị mà có thể xử lý yêu cầu đó. Nếu chỉ gửi *Intent* sẽ không có cái nào phù hợp cả, app bị crash

Để xác thực rằng một *Activity* hoặc thành phần khác có khả năng nhận *Intent* hay không, sử dụng phương thức `resolveActivity()` với hệ thống quản ly package như sau:
```java
if (sendIntent.resolveActivity(getPackageManager()) != null) {
	startActivity(chooser);
}
```

### Hiển thị app lựa chọn
Để tìm *Activity* hoặc thành phần mà có thể xử lý yêu cầu *Intent*, hệ thống Android kết nối *Intent* với các *Activity* mà *Intent filter* chỉ thị, người dùng sẽ được hiển thị một app chọn để lựa chọn cái nào có thể handle *Intent*
```java
Intent sendIntent = new Intent(Intent.ACTION_SEND);
String title = getResources().getString(R.string.chooser_title);
Intent chooser = Intent.createChoose(sendIntent, title);

if (sendIntent.resolveActivity(getPackageManager()) != null) {
	startActivity(chooser);
}

```

### Nhận một implicit Intent
Muốn nhận một implicit *Intent*, bắt buộc phải khai báo một hoặc nhiều *Intent filter* bên trong `AndroidManifest.xml`. Với mỗi *Intent filter* chỉ định loại *Intent* nó chấp nhận dựa vào *action, data và category* của *Intent*. Hệ thống chỉ phục vụ implicit *Intent* với app khi vào chỉ khi nó có thể thông qua được *Intent filters*

>**NOTE** : Explicit Intent luôn luôn được phục vụ tới mục tiêu, kể cả có bát kì *Intent filter* nào được khai báo. Nếu một *Acitivity* không có *Intent* filter, nó chỉ có thể bắt đầu bởi một *explicit Intent*

### Intent filter
Định nghĩa *Intent filter* với một hoặc nhiều thẻ <intent-filter/> trong file `AndroidManifest.xml`, bao bọc  bên trong là <activity/> tương ứng.
Một *Intent filter* có thể chứa các thành phần sau, tương ứng với các trường có trong *Intent obejct* được miêu cả bên dưới
- <action/> : Hành động mà *Activity* sẽ chấp nhận
- <data/> : Loại dữ liệu được chấp nhận, bao gồm MIME hoặc các thuộc tin của dữ liệu URI
- <category/> : Intent category

```xml
<intent-filter>
	<action android:name="android.intent.action.MAIN"/>
	<category android:name="android.intent.category.LAUNCHER"/>	
	<data android:mimeType="text/plain"/>
</intent-filter>
```

Nếu muốn chỉ định nheieuf hơn một action, data hoặc là category với cùng một *Intent filter* hoặc có nhiều *Intent filter* ở mỗi *Activity* để có thể xử lý từng loại

## Actions
*Intent filter* có thể khai báo 0 hoặc nhiều <action/>.  *Action* được định nghĩa là tên của thuộc tính, và chứa chuỗi `"android.intent.action"` cộng với tên của *Intent action* mà không lấy phần `ACTION_`
Ví dụ về *Intent filter* mà đúng với *ACTION_EDIT* và *ACTION_VIEW*
```xml
<intent-filter>
	<action android:name="android.intent.action.EDIT"/>
	<action android:name="android.intent.action.VIEW"/>
</intent-filter>
```

## Categoris
*Intent filter* có thể khai báo 0 hoặc nhiều <category/>. Thẻ này được định nghĩa trong thuộc tính tên, và chứa chuỗi `"android.intent.category"` cộng với tên của category trừ đi phần tiền tố `CATEGORY_`
Vis dụ dưới đây đúng với `CATEGORY_DEFAULT` và `CATEGORY_BROWSABLE`:
```xml
<intent-filter>
	<category android:name="android.intent.category.DEFAULT"/>
	<category adnroid:name="andorid.itnent.category.BROWSABLE"/>
</intent-filter>
```

> **NOTE** Bất kì *Activity* muốn chấp nhận *implicit Intent* bắt buộc phải bao gồm `android.intent.category.DEFAULT`


## Data
*Intent filter* có thể khai  báo 0 hoặc nhiều <data/> dành cho URI bao gồm trong *Intent data*. *Intent* có thể chấp nhận nhiều loại dữ liệu bao gồm:
- URI Scheme
- URI Host
- URI Path
- Mime type

Ví dụ về *Intent filter* kết nôi bắt kì Intent nào có dữ liệu với URI http và "image/mpeg" hoặc "audio/mpeg"
```xml
<intent-filter>
	<data android:mimeType="video/mpeg" android:scheme="http"/>
	<data android:mimeType="audio/mpeg" android:scheme="http"/>
</intent-filter>
```

## Chia sẻ dữ liệu sử dụng ShareCompat.IntentBuilder
Sử dụng để chia sẻ items có trong app với mạng xã hội và các ứng dụng khác. Mặc dù có thể xây dựng một share action trong app sử dụng *implicit Intent* với hành động `ACTION_SNED`, Android cung cấp `ShareCompat.IntentBuilder` hỗ trợ triển khai chia sẻ dễ dàng trong ứng dụng
>**NOTE**: Ứng dụng mà mục tiêu dành cho các bản Andorid sau API 14, có thể sử dụng ShareActionProvider để chia sẻ hoạt động thay vì ShareCompat.IntentBuilder.

Với `ShareCompat.IntentBuilder`, không cần phải tạo và gửi một *implicit Intent* để có thể chia sẻ hành động. Sử dụng phương thức có trong `ShareCompat.IntentBuilder` để chỉ ra dữ liệu bạn muốn chia sẻ cũng như là các thông tin thêm. Bắt đầu với phương thức`from()` để tạo một *Intent builder*, thêm các phương thức khác để có thể thêm nhiều dữ liệu, và kết lúc bằng phương thức `startChooser()` để tạo và gửi *Intent*. Bạn có thể xâu chuỗi các phương thức lại với nhau:
```java
ShareCompat.IntentBuilder
	.from(this) // thông tin về Activity bắt nguồn
	.setType(mimeType) // kiểu dữ liệu xử lý
	.setChooserTitle("Share this text with: ") // title dành cho app chooser
	.setText(txt) /// intent data
	.startChooser()
```

## Quản lý task
Task dành cho ứng dụng của bạn chứ một stack, bên trong nó có các *Activity* người dùng đã từng dùng trong quá tình sử dụng app. Khi người dùng di chuyển xung quanh app, *Activity* dành cho *Task* sẽ được đẩy và và đưa ra stack 

## Activity launch mode
Sử dụng *Activity* launch mode để chỉ ra các một *Activity* mới nên được đối xử khi khởi chạy, nó nên được thêm vào *Task* hiện tại hay là khởi chạy trong một *Task* mới. Định nghĩa chế độ khởi chạy dành cho *Activity* voiwss thuộc tính bên trong thẻ <activity/> trong file `AndroidManifest.xml` hoặc là cờ được bật ở *Intent* sử dụng để chạy *Activity*

### Các thuộc tính của thẻ <activity/>
```xml
<activity
	android:name=".SecondActivity"
	android:lable="@string/activity2_name"
	android:parentActivityName=".MainActivity"
	adnroid:launchMode="standard"
/>
```

Có 4 chế độ chạy có sẵn
- `standard` : *Activity* mới được chạy và thêm vào *back stack* cho *Task* hiện tại. Một *Activity* có thể bị khởi tạo nhiều lần, *Task* đơn có thể chứa được nhiều *instance* của cùng *Activity*, và nhiều *instance* có thể thuộc về nhiều task khác nhau
- `singleTop`: Nếu một *instance* của một *Activity* đã tồn tại ở trên cùng của *back stack* ở *Task* hiện tại và một *Intent* yêu cầu *Activity* đó đến, **Andorid** định hướng *Intent* đó đến *instance* hiện tại của *Activity* hơn là tạo một một *Activity* mới. *Activity* vẫn sẽ được khởi tạo instance mới nếu như đã tồn tại *Acitivity* ở trong *back stack* nhưng không phải ở top
- `singleTask`: Khi *Activity* được khở tạo, hệ thống tạo mới *Task* dành cho *Activity*. Nếu *Task* khác đã tồn tại với một *instance* của *Activity*, hệ thống sẽ định hướng *Intent* đến *Activity* đó
- `singleInstance`: Cũng giống như `singleTask`, ngaoij trừ hệ thống sẽ không khởi chạy bất cứ *Activity* nào vào *Task* đang nắm dữ *Activity*. *Activity* luôn luôn là duy nhất và chỉ là thành phần của *Task* đó

### Intent flags
Tùy chọn để chỉ ra các *Activity* nhận *Intent* nên xử lý *Intent* như thế nào. *Intent flags* được định nghĩa như là các hằng số bắt đầu bằng từ `FLAG_`. Bạn thêm *Intent flags* vào một *Intent objects* bằng `setFlag()` hoặc là `addFlag()`

3 lại *Intent flag* riêng biệt được sử dụng để điều khiển chế độ khởi chạy của *Activity*. Sử dụng *Intent flag* sẽ được ưu tiên hơn so với config launchMode bên trong `AndroidManifest.xml` trong trường hợp bị xung đột
- `FLAG_ACTIVITY_NEW_TASK`: bắt đầu *Activity* trong một task mới. Hành vi này giông như `singleTask` trong launchMode
- `FLAG_ACTIVITY_SINGLE_TOP`: nếu *Activity* được khởi chạy ở trên cùng của *back stack*, điều hướng *Intent* tới *Acitivity* instance. Ngược lại sẽ tạo một *Acitivity* instance mới. Hành vi này giống như `singleTop` trong launchMode
- `FLAG_ACTIVITY_CLEAR_TOP`: nếu một instance của *Activity* được khởi chạy đã tồn tại trong *back stack*, phá hủy bất kì *Activity* nào đang ở trên top và định hướng *Intent* tới instance đã tồn tại. Khi sử dụng kết hợp với `FLAGE_ACTIVITY_NEW_TASK`, cờ này tìm ra *instance* đã tồn tại trong bất kì *Task* nào và đưa chúng trở lại hoạt động

### Xử lý Intent
Khi được hệ thống Android định hướng tới một *Activity* đã tồn tại, hệ thống sẽ gọi phương thức `onNewIntent()`. Phương thức này bao gồm tham số dành cho *Intent* mới đã được định huowgns tới *Activity*. Override phương thức này để có thể xử lý thông tin từ *Intent* mới

>**NOTE** phương thức `getIntent()` sử dụng để có thể truy cập *Intent* đã được sử dụng để khởi tạo *Acitivty* - luôn luôn giữ lại *Intent khởi nguồn* sử dụng để chạy *Activity*. Gọi phương thức *setIntent()* trong phương thức *onNewIntent*()*

```java
@Override
public void onNewIntent(Intent intent) {
	super.onNewIntent(intent);
	// Sử dụng Intent mới, không phải là intent ban đầu chạy Activity
	setIntent(intent);
}
... // somewhere in activity
getIntent() // -> lúc này sẽ trả về Intent mới, không phải Intent ban đầu nữa

```

## Quan hệ các Task
Quan hệ Task chỉ ra task nào *Acitivity* thuộc về khi mà *Activity instance* được chạy. Mặc định mỗi *Acitivity* sẽ thuộc về ứng dụng mà đã khởi chạy nó. Một *Activity* từ bên ngoài ứng dụng, khởi chạy với một *implicit Intent* thuộc về ứng dụng mà đã gửi *implicit Intent* đó

Để định nghĩa quan hệ *Task*, thêm thuocj tính `android:taskAffinity` vào trong thẻ <activity/>. Mặc định quan hệ sẽ là tên gói dành cho ứng dụng. 
```xml
<activity
   android:name=".SecondActivity"
   android:label="@string/activity2_name"
   android:parentActivityName=".MainActivity"
   android:taskAffinity="com.example.android.myapp.newtask">
   <!-- More attributes ... -->
</activity>
```

Quan hệ *Task* thường sử dụng với chế độ khởi chạy *singleTassk* hoặc là cờ `FLAG_ACTIVITY_NEW_TASK` để đặt một *Acitivity* vào một cái task được đặt tên của chính nó. Nếu *Task* đã tồn tại, *Intent* được định hướng tới *Task* đó và quan hệ đó ???

