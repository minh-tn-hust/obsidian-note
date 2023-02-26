Một service là một thành phần thức hiện các hoạt động dài, thường sử dụng trong background. Không giogons như *Activity*, một *Service* không cần cung cấp giao diện người dùng. *Service* được định nghĩa bằng lớp *Serivce* hoặc một lớp con của nó
Một service có thể bắt đầu, ràng buộc, hoặc cả hai:
- Một *started service* là một service mà thanh fphanaf app bắt đầu bằng việc gọi `startService()`
Sử dụng các started service dành cho những *Task* chạy nền để tiền hành các hoạt động tốn thời gian. Cũng có thể sử dụng started serivces dành chó các *Task* tiền hành công việc dành cho các quá trình xử lý từ xa
- Một *bound serivce* là một serivce mà một thành phần app có thể ràng buộc với nó bằng cách gọi `bindService()`

Sử dụng *bound service* dành cho các *Task* mà các thành phần của app khác tương tắc với để thực hiện các giao tiếp giữa các quá trình (IPC). Ví dụ, một *bound serivce* có thể xử lý gia dịch mạng, thực hiện các file I/O, chạy nhạc, tương tác với database

Một service chạy trên luồng UI mà thực hiện xử lý nó - *Service* không được tạo riêng một luồng, và không được chạy riêng rẽ với quá trình xử lý cho tới khi bạn chỉ định cho nó

Nếu *Service* của bạn làm bất kì công việc nào chiếm dụng CPU hoặc là block các toán tử (Ví dụ như chạy file MP hoặc là mạng), tạo một luồng mới mà bên trong đó service sẽ chạy. Bằng cách sử dụng luồng riêng biệt, vạn giảm thiểu rủi ro người dùng nhìn thấy looix "application not responding", và luồng chính của app cũng cần được để lại để người dùng tương tác với các *Activity*

Để triển khai bất kì loại dịch vụ nào trong ứng dụng, làm theo các bước sau
1. Khai báo service trong manifest
2. Kế từa lớp `Service` ví dụ như `IntentSrevice` và tạo code triển khai
3. Quản lý vòng đời service

## Khai báo service trong file Manifest
Giống như với *Activity* và các thành phần khác, bạn khải khai báo tất cả các ịch vụ trong file AndroidManifest. Để khai báo một dịch vụ, thêm thẻ <serivce/> như là một thành phần con của <application/>
```xml
<manifest ... >
	...
	<application ... >
		<serivice android:name="ExampleService" android:exported="false"/>
		...
	</application>
</manifest>
```

Để khóa truy cập vào mọt service từ một app khác, khai báo dịch vụ với thuộc tính private.  Để làm điều này, set trường `android:exported` là false. 

## Started service
Cách để một dịch vụ bắt đầu
1. Một thành phần App ví dụ như *Activity* gọi `startService()` và truyền vào một *Intent*. *Intent* chỉ định dịch vụ và bao gồm bất kì thông tin gì cho service sử dụng
2. Hệ thống gọi phương thức `onCreate()` và bất kì những callback đặc biệt nào trong luồng chính. Tùy thuốc vào dịch vụ để triển khai các callback với các hành vi phù hợp, ví dụ tạo một luồng mới để làm việc
3. Hệ thống gọi phương thức `onStartCommand()`, truyền vào *Intent* được cung cấp bởi bước 1

Một khi bắt đầu, một service có thể chạy nền, kể cả nếu component bắt đầu nó bị phá hủy. THường thường, *started service* thực hiện hành động đơn, và không trả về kết quả để gọi. Ví dụ, nó có thể downlado hoặc uploda filt thống qua mạng. Khi xử lý xong, service nên dừng lại bằng cách gọi `stopSeflt()` hoặc một thành phần khác có thể dùng nó bằng cách gọi `stopService()`

Cụ thể, giả sử một *Activity* cần để sưu dữ dữ liệu tới một cơ sở dữ liệu online. *Activity*  bắt đầu một dịch vụ đồng hành bằng cách truyền một *Intent* vào `startService()`. Service nhận được intent trong phương thức `onStartCommand()`, kết nối với internet, và thực hiện giao dịch chuyển duef liệu. Khi giao dịch xong, service tự đống lại bằng cách sử dụng `stopSelf()` và tự phá hủy


## Intent serivce

Hầu hetes cả *started servicve* không cần phải xử lý nhiều yêu cầu dồng thời, nếu chúng phải làm như thế, nó có thể làm một kịch bản đa luồng phức tạp và dễ lỗi. Do những lý do nhày, lớp *IntentService* là một lớp con hữu dụng cho *Service* dự trên dịch vụ của bạn:
- *IntentService* tự động cung cấp các luồng công nhân để xư lý *Intent*
- *IntentService* xử lyus một vài code lắp mà các dịch vụ thông thường cầm.
- *IntentService* có thể tạo một hàng chờ các công việc và truyền từng intent một vào triển khai `onHandleIntent()`, bạn không cần phải lo lắng về đa luồng

Để triển khai *IntentService*
1. Cung cấp một constructor cho Service
2. Tạo một triển khai của `onHandleIntent()` để thực hiện việc mà client cung cấp
```java
public class HelloIntentService extends IntentService {
	// Cái này yêu cầu phải có và để gọi lên lớp cha
	// dành cho luồng công nhân
	public HelloIntentService() {
		super("HelloIntentService");
	}

	@Override
	protected void onHanleIntent(Intent intent) {
		try {
			Thread.sleep(5000);
		} catch (InterruptedException e) {
			Thread.currentThread().interrupt();
		}
	}

	
}
```


## Bound serivces
Service là ràng buộc khi các thành phần app bị buộc vào nó bằng cách gọi `bindService()`. Một *bound service* yêu cầu mộojotgiao diện client-server mà cho phpes các thành phần có thể tương tác với service, gửi request, và lấy kết quả, thỉnh thoảng sử dụng giao tiếp giữa các xử lý để gửi và nhận các thông tin giữa các xử lý với nhau. Một *bound service* chỉ chạy miễn là có một thành phần ứng dụng khác được ràng buộc với nó. Nhiều thành phần có thể ràng buộc tới một service một lần, nhưng khi tất cả chúng dudocj bỏ ràng buộc, service sẽ bị hủy

Một bound serivce thông thường không cho phép các thành phần bắt đầu nó bằng việc gọi `startService()`



## Triển khai service ràng buộc
Để triển khai các service ràng buộc, định nghĩa một giao diện mà chỉ ra các client có thể giao tiếp với service. Giao diện này, service của bạn trả về từ callback `onBind()`, chỉ triển khai `IBinder`.

Để truy xuất giao diện `IBinder`, một thành phần ứng dụng khách gọi `bindService()`. Một khi client nhận được `IBinder` client tương tác với service thông qua interface

Có nhiều cách để triêng khai service ràng buộc, và việc triển khai phức tạp hơn so với *started service*.

## Binding to a service
Để ràng buộc một service được khai báo trong manifest và triển khia nó trong mọt thành phần của app, sử dụng `bindService()` voisws một *Itnent* tường mình

## Life cycle
Cái này đơn giản hơn lifecycel của *Activity* tuy nhiền, nó lại quan trong hơn và bạn phải chú ý nhiêu fhonw để service được tạo và phá hủy. Bởi vì một services không có UI, service có thể tiếp tục chạy ngầm với khong cách nào người dùng biết, thâm chí nếu người dùng chuyển sang một app khác, trong trường hợp này vẫn có thể chiếm dụng tài nguyên và là cạn pin thiết bị

Tương tự như *Activity*, một service có các phương thức lifecycel mà bạn chó thể triển khai để mô hình thay đổi trạng thái của state và thực hiện công việc tại tác thời gian phù hợp. Khung service triển khai dưới đây mô tả các phương thức life-cycle

```java
public class ExampleService extends Service {
	int mStartMode; // chỉ ra hành vi mà service bị hủy
	IBinder mBinder; // giao diện client được ràng buộc
	boolean mAllowRebind; // chỉ ra các mà onRebind có thể làm
	@Override
	public void onCreate() {
		// Service được tạo	
	}

	@Override
	public int onStartCommand(Intent intent, int flags, int startId) {
		// Service bắt đầu, bowir vậy gọi startService
		return mStartMode;
	}

	@Override
	public IBinder onBind(Intent intent) {
		// Client ràng buộc tới Service với bindService
		return mBinder;
	}

	@Override
	public boolean onUnbind(Intent intent) {
		// Tất cả các client hủy ràng buộc với unbindService()
		return mAllowRebind;
	}

	@Override
	public void onRebind(Intent intent) {
		// Client ràng buộc service với bindService() sau khi 
		// onUnbind() sẵn sàng để gọi
	}

	@Override
	public void onDestroy() {
		// Service không còn được sử dụng và bị phá hủy
	}

}
```

## Lifecycle của started services so với bound services
Service ràng buộc chỉ tồn tại để phục vụ thành phần app mà nó được ràng buộc, khi không có thành phần nào được ràng buộc với service, hệt hống sẽ phá hủy nó. Service ràng buộc không cần phải dừng lại một cách tường minh như *started service* (sử dụng `stopService()` hoặc `stopSelf()`)

Biểu đồ dưới dây chỉ ra sự so sánh giữa vòng đời của started và buond service
![Started and Bound Service Lifecycle, noborder](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/7-4-c-services/dg_service_lifecycle.png "Started and Bound Service Lifecycle, noborder")

## Foreground service
Trong khi hầu hết các services chạy background, một vài thứ chạy foreground. Foreground service là một service mà người dùng có thể chú ý nó đang chạy. Mặc dù cả *Activity* và *Service* có thể bị hủy nếu như system hết bộ nhớ, một foreground service có độ ưu tiên hơn các nguồn tài nguyên khác
 Ví dụ, một trình chạy nhác chyaj nhạc từ một service nên được thiết lập để chạy foreground, bởi vì người dùng có thể chú ý được hành động đó. Thông báo trên thanh trạng thái nên chỉ ra bài hát hiện tại và cho phép nugoiwf dùng khởi chạy *Activity* để tương tác với trình tạo nhạc
Để yêu cầu một service chạy trong foreground, gọi `startForeground()` thay vì `startService()`. Phương thức này nhận vào 2 tham số: một integer đọc nhất để định danh thông báo và một đối tượng *Notification* dành cho thanh trạng thái. Thông báo này là uông chạy, nghĩa là nó không thể bị từ chối. Nó luông nằm trên thanh trạng thái cho tới khi service bị dừng và xóa bỏ khỏi foreground.
Ví dụ
```java
Intent notificationIntent = new Intent(this, ExampleActivity.class);
PendingIntent pendingIntent = PendingIntent.getActivity(this. 0, notificationIntent, 0);
Notification notification = new Notification.Builder(this, CHANNEL_DEFAULT_IMPORTANCE)
	.setContentTitle(getText("notification_title"))
	.setContentText(getText("notification_message"))
	.getSmallIcon(R.drawable.icon)
	.setContentIntent(pendingIntent)
	.setTicker(getText(ticker_text))
	.build();

startForeground(ONGOING_NOTIFICATION_ID, notification);
```

Để xoa service khởi foreground, gọi `stopForeground()`. Phương thức này nhận vào một biến boolean, chỉ ra rằng xóa thông báo khỏi thanh trạng thái. Phương thức này không dừng service. Tuy nhiên nếu bạn dừng service tỏng khi nó vẫn đang chạy foreground, sau đó notificaitn cũng sẽ được remove



