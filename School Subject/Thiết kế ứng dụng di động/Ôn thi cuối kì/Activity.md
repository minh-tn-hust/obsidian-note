
# Activity
>biển diễn một màn hình đơn lẻ có trong app của mình có trong app với một giao diện mà người dùng có thể tương tác được

App được cấu tạo bởi tập các activity. Mỗi *Activity* hoạt động độc lập với các *Activity* khác
Điều này cho phép app của mình có thể bắt đầu một *activity* ở app khác và ngược lại
Trong một App luông có một hoạt động được chỉ định là hoạt động chính, ví dụ như **MainActivity**. Người dùng thấy hoạt động chính khi mà bật app lên ở lần đầu tiên. 

## Note 1
Khi một *activity* mới bắt đầu, activity trước đó sẽ bị dừng lại (hệ thống giữ *activity* đó bên trong stack), khi người dùng xong *activity* hiện tại và bấm nút *Back*, hoạt động sẽ được lấy ra khỏi stack và hủy, hoạt động trước đó lại được tiếp tục

## Note 2
Khi triển khai một Activity, phải luôn luôn triển khai phương thức *onCreate* - đây là phương thức sử dụng để khởi tạo các component cần thiết của *Activity*

## Note 3
Khi *setContentView* được gọi cùng với đường dẫn của file layout, hệ thống sẽ tạo ra tất cả các view khởi đầu từ layout được chỉ định và thêm chúng vào bên trong *Activity*. Quá trình này được gọi là inflating

## Note 4
Mỗi *Activity* trong app phải được khai báo trong *AndroidManifest.xml*, bên trong thẻ <activity/> ở thẻ <application/>

```xml
<activity android:name=".MainActivity" >
   <intent-filter>
      <action android:name="android.intent.action.MAIN" />
      <category android:name="android.intent.category.LAUNCHER" />
   </intent-filter>
</activity>
```

Thẻ <activity/> bao gồm một số thuộc tính để định nghĩa các đặc tính của một *Activity* ví dụ như label, icon, hoặc theme.  Thuộc tính cần thiết nhât chính là *androi:name*

Thẻ <activity/> có thể khai báo *Intent* filter - chỉ định loại *Intent* mà *Activity* sẽ chấp nhận
```xml
<intent-filter>
	<action android:name="android.intent.action.MAIN"/>
	<category android:name="android.intent.category.LAUNCHER"/>
</intent-filter>
```

*Intent* filter bắt buộc phải bao gồm ít nhât một thẻ <action/> và cũng có thể bao gồm một thẻ <category/> và tùy chọn thẻ <data/>

Thẻ <category/>> chỉ định rằng *Activity* có thể được liệt kê trong hệ thống khởi chạy ứng dụng

Mỗi *Activity* trong app cũng có thể được khai báo *Intent* filter, nhưng chỉ có *MainActivity* được khai báo hành động **main**

