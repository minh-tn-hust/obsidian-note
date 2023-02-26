## onCreate
*Activity* bước vào trạng thái khởi tạo khi nó được bắt đầu trong lần đầu tiên. Khi một *Acitivity* được khởi tạo lần đầu tiên, hệ thống gọi phương thức `onCreate()` để khởi tạo *Activity* đó. 
Đây là phương thức bạn bắt buộc phải triển khai trong một *Activity*. Trong `onCreate()` bạn có thể thực hiện những logic khởi tạo cơ bản và nó nên xẩy ra chỉ một lần như là khởi tạo các biến toàn scope, cài đặt các nhiệm vụ background

Đây là một trạng thái tạm thời, *Activity* tồn tại trong trạng thái khởi tạo chỉ dài ~ chạy phương thức `onCreate()`

## onStart
Sau khi *Activity* được khởi tạo với `onCreate()`, hệ thống gọi phương thức `onStart()`, và *Activity* ở trạng thái bắt đầu. 

Phương thức `onStart()` cũng được gọi nếu như một *Activity* đã dừng trở lại chạy, ví dụ như người dùng click vào nút *Back* hoặt là nút *Up* để trở về màn hình trước. Phương thức `onStart()` cos thể được gọi nhiều lần trong suốt vòng đời của *Activity*

Khi một *Activity* trong trạng thái kohwir tạo và hiển thị trên màn hình, người dùng không thể tương tác với nó cho tới khi`onResume()` được gọi.

Trạng thái này alf một trạng thái tạm thời. Sau khi bắt đầu, *Activity* di chuyển vàm trạng thái tiếp tục

## onResume
*Activity* trong trạng thái tiếp tục khi mà nó đã được khởi tạo, thấy được trên màn hình và sẵn sàng để sử dụng. Trạng thái tiếp tục thường được gọi là trạng thái chạy, bởi vì nó trong trạng thái này, người dùng thực sự tương tác với app

Lần đầu tiên *Activity* được hệ thống bắt đuầ gọi phương thức `onResume()` chỉ ngay sau `onStart()`. Phương thức `onResume()` có thể được gọi nhiều lần, mỗi lần ứng dụng quay trở lại từ trạng thái tạm dừng (paused)

*Activity* tồn tại trong trạng thái tiếp tục trong suốt quá trình *Activity* ở foreground và người dùng đang tương tác với nhó. Từ trạng thái tiếp tục, *Acitivity* có thể di chuyển sang trạng thái tạm dừng

## onPause
Trạng thái tạm dừng có thể xảy ra trong một vài tình huống:
- *Activity* đi vào background, nhưng chư dừng hoàn toàn.  Đây là dầu hiệu đầu tiên mà người dùng rời khỏi *Activity*
- *Acitivity* chỉ hiển thị một phần trên màn hình bởi vì một hội thoại/một *Acitivity* khác đang nằm bên trên nó
- Trong chế độ nhiều cửa sổ hoặc là chia màn hình (API 24), *Activity* hiển thị trên màn hình nhưng *Activity* khác được người dùng tập trung vào

`onPause()` nên được thực thi nhanh chóng. Đừng sử dụng `onPaus()` dành cho các hoạt động chiến dụng CPU như là đọc ghi data vào cơ sở dữ liệu. App có thể vẫn còn hiển thị trên màn hình khi mà nó chuyển qua trạng thái tạm dùng, nhưng bất kì sự chậm trễn nào trong quá trình thực thi `onPause()` có thẻ làm chậm chuyển cảnh của người dùng tới *Activity* khác.

## onStop
*Activity* ở trạng thái dừng khi nó không được nhìn thấy trên màn hình. Thường bởi vì nugoiwf dùng bắt đàu một *activity* khác hoặt là người dùng trở về màn hình home. Hệ thoongas Android giữ lại thể hiện của *Activity* trong back stack, và nếu người dùng trở lại *Acitivity*, hệ thống sẽ tái hởi động nó. Nếu như tài nguyeentaaps, hệ thống có thẻ kill luôn một *actitivy* đang trong trạng thái dừng hoàn toàn

## onDestroy
Khi *Activitiy* bị phá hủy, nó được tắt hoàn toàn và thể hiện của *Activity* sẽ được hệ thống lấy lại. Điều này có thể xảy ra trong một vài trường hợp:
- Khi thực hiện gọi phương thức `finish()` để thủ công tắt nó đi
- Người dùng trả về *Activity* trước đó
- Thay đổi tinh chỉnh thiết bị xảy ra

`onDestroy()` hoàn toàn dọn dẹp *Activity* bởi vậy không có thành phần nào (ví  dụ như một luồng) có thẻ chạy sau khi *Activity* bị phá hủy

## onRestart
Là một trạng thái tạm thời và chỉ xảy ra khi một *Activity* đã dừng được bắt đầu trở lại. Trong trường hợp `onRestart()` được gọi giữa `onStop()` và `onStart()`. Nếu bạn co tài nguyên mà cần phải dừng / bắt đầu, bạn có thẻ triển khia hành vi đó trong onStop() hoặc là onStart() hơn là onRestart()


## Thiết lập thiêt bị bị thay đổi
- Quay thiết bị
- Thay đổi ngôn ngữ hệ thống
- Người dùng sử dụng chế độ nhiều cửa sổ

Activity sẽ được phá hủy và sau đó sẽ khởi tạo lại. Flow như sau
1. onPause()
2. onStop()
3. onDestroy()
4. onCreate()
5. onStart()
6. onResume()

## Trạng thái của thể hiện *Activity*
Khi một *Activity* được khởi tọa lại, trạng thái của *Activity* và bất kì xử lý nào của User trong *Activity* sẽ bị mất hoàn ttoanf, với một số trường hợp ngoại lệ như sau:
- Một vài thông tin trạng thái của *Acitivity* được mặc định tự động lưu. Trạng thái của các thành phần *View* với ID độc nhất (được định nghĩa bởi thuộc tính `android:id`) được lưu và phục hồi khi *Activity* được khởi tạo lại
- *Intent* sử dụng để bắt đầu *Activity* và thông tin được lưu trữ trong *data* hoặc là *extras*, luôn sẵn sàng cho *Activity* khi nó được khởi tạo lại

Trạng thái của *Activity* được lưu như là một cặp key/value trong một đối tượng *Bundle* gọi là *Activity instance state*. Hệ htoongs mặc định lưu thông tin trạng thái vào Bunle chỉ ngày turocs khi *Activity* bị dừng lại, và đẩy nó sang một *Activity instance* mới để phục hồi

Có thể thêm instance data của mình vào instance state *Bundle* bằng cách override lại phương thức `onSaveInstanceState`. Trạng thái *Bunle* được ném tới phương thức `onCreate` để có thể phục hồi lại *instance state* khi *Activity* được khởi tạo. `onSaveInstanceState` sẽ được gọi khi mà người dùng rời khởi *Activity* (thỉnh thoảng trước khi phương thức `onStop()`)

```java
// Lưu trạng thái
public void onSaveInstanceState(Bundle savedInstanceState) {
	super.onSaveInstanceState(savedInstanceState);
savedInstanceState.putInt("score", mCurrentScore);
savedInstanceState.putInt("level", mCurrentLevel);
}
```

### Phục hồi lại state
```java
protected void onCreate(Bundle savedInstanceState) {
	// Luôn luôn gọi superclass trước
	super.onCrate(savedInstanceState);
	// Kiểm tra nếu như lần khởi tạo trước phá hủy instance
	if (saveInstanceState != null) {
		mCurrentScore == savedInstanceState.getInt("score");
		mCurrentLevel = saveInstanceState.getInt("level");
	}
} else {
	// Khởi tạo các thành phần với giá trị mặc định
}

```