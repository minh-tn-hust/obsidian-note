Luồng công nhân là bất kì luồng nào không mải luồng chính hoặc luồng UI. Sử dụng lớp AyncTassk để triển khai các task bất dồng bộ hoặc các task chạy tốn thời gian trên một luồng ocong nhân. AsyncTassk cho phép thực hiện các thao tác ngầm trong luồng công nhân và công bố kết quả cho luồng UI mà không cần phải định hướng điều khiển luồng hoặc handle

## Khi một AsyncTask được thực hiện, nó sẽ đi qua 4 bước sau:
1. onPreExcute() được gọi trên luồng UI trước khi task được thực thi. Trong bước này, thông thường sử dụng để setup *Task*, chẳng hạn bằng cách hiển thị thanh xử lý
2. `doInBackgourd(Params...)` được gọi trong luồng *background* ngay lập túc sau khi `onPreExecute()` hoàn thành. Bước này thực hiện các tính toán ngầm, và trả về một kết quả, và đẩy kết quả tới `onPostExecute()`. Phương thức `doInBackground()` cũng có thể gọi `publishProgress(Progress...)` để xuất bản một hoặc một vài đơn vị xử lý
3. `onProgressUpdate(Progress...)` chạy trong luồng UI sau khi `publishProgress(Progress...)` được gọi. Sử dụng `onProgressUpdate()` để báo cáo bất kì hình thức xử lý tới luồng UI trong khi tính toán ngầm đang được thực thi. Ví dụ, bạn có thể sử dụng nó để đẩy dữ liệu tới animation xử lý thanh hoặc là show log
4. `onPostExecute(Result)` chạy trên luồng UI sau khi các tính toán ngầm hoàn thành. Kết quả của tính toán ngầm được đẩy vào phương thức này như là một tham số![Diagram for method calls of an AsyncTask, noborder](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/7-1-c-asynctask-and-asynctaskloader/dg_asynctask.png "Diagram for method calls of an AsyncTask, noborder")
## Cách sử dụng
Để sử dụng lớp `AsyncTask`, định nghĩa một lớp con của `AsyncTask` và override hàm `doInBackground(Params)` (và thường cả `onPostExecute(Result)`)

## Các tham số của AsyncTask
Trong lớp con của `AsyncTask`, cung cấp các kiểu dữ liệu dành cho 3 loại tham số sau
- *Params* chỉ định kiểu tham số đẩy vào phương thức `onInBackground()` như là một cái mảng
- *Progress* chỉ định kiểu của các tham số đẩy vào *publishProgress()* trong luồng *background*. Những tham só này được đẩy vào *onProgressUpdate()* trong luồng UI
- *Result* chỉ định kiểu của tham số mà khi `doInBackgroud()` trả về. Tham số này thường được đẩy tới `onPostExecute()` trong luồng UI

Chỉ đinh một kiểu dữ liệu cho mỗi các tham số, sử dụng `Void` nếu tham số đó không được sử dụng. Ví dụ
```java
public class MyAsyncTask extends AsyncTask <String, Void, Bitmap> {

}
```
Công thức để khai báo kiểu dữ liệu dành cho một AsyncTask
```java
public class TÊN_ASYNC_TASK extends AsyncTask<Kiểu_dữ_liệu_Params, Kiểu_dữ_liệu_Progress, Kiểu_dữ_liệu_Result> {}
```

Ví dụ cụ thể
```java
private class DownloadFilesTask extends AsyncTask<URL, Integer, Long> {
	// Khi task được thực thi, sẽ gọi hàm này đầu tiên
	protected Long doInBackground(URL... urls) {
		int count = urls.length;
		long totalSize = 0;
		for (int i = 0; i < count; i++) {
			totalSize += Downloader.downloadFile(urls[i]);
			publishProgress((int) ((i / (float) count) * 100*));
			if (isCancelled()) break;
		}
		retrun totalSize;
	}
	protected void onProgressUpdate(Integer... progress) {
		setProgressPercent(progress[0]);
	}
	protected void onPostExecute(Long result) {
		showDialog("Downloaded " + result + " bytes")	;
	}
}
```

## Thực thi một AsyncTask
Sau khi định nghãi lớp con của AsyncTask, khởi tạo nó trong luồng UI. Sau đó thực hiện gọi phương thức `execute()` trong instance của nó. Đẩy vào các tham số. (Những tham só này tương ứng với tham số đã thảo luận ở trên)
Ví dụ, để thực thi `DownloadFilesTask` định nghĩa ở trên, sử dụng dòng code dưới đây
```java
new DownloadFilesTask().execute(url1, url2, url3);
```

## Hủy AsyncTask
Bạn có thể hủy task bất cứ lúc nào, từ bất cứ luồng nào bằng cách gọi `cancel()`
- Phương thức này trả về `false` nếu như task không thể hủy, tiêu biểu bởi vì nó đã được haonf thành. Còn không thì nó sẽ trả về `true`
- Để tìm một task đã bị hủy, sử dụng  `isCancelled()` để check từ `doInBackground(Object[])`, ví dụ từ bên trong vòng lặp được show ở bên dưới.
- Sau khi một `AsyncTask` bị hủy, `onPostExecute()` sẽ không được gọi sau khi `doInBackground()` trả về. Thay vì đó, `onCancelled(Object)` được gọi.  Triển khai mặc định của `onCancelled(Object)` gọi `onCancelled()` và không quan tâm tới kết quả

## Giới hạn của AsyncTask
Không áp dụng cho một vài trường hợp sau
- Thay đổi config thiết bị gây ra vấn đề
>Khi thay đổi config của thiets bị trong khi `AsyncTask` đang chạy, *Activity* tạo ra `AsyncTask` bị phá hủy, và AsyncTask đã được tạo sẽ không thể truy cập được ở *Activity* mới, kết quả của *AsyncTask* sẽ không được công bố
- `AsyncTask` làm tràn bộ nhớ nếu như người dùng thoát app mà không gọ `cancel()`

# Loaders
*Background task* thường được sử dụng để lấy dữ liệu như là báo cacso thời tiết hoặc là review phim. Tải dữ liệu có thể chiếm dụng nhiều bộ nhớ, bạn muốn dữ liệu luôn sẵn sàng ngay cả khi thay đổi cài đặt thiết bị. Dành cho những trường hợp này, sử dụng loader, class tạo ra cho sự thuận tiên về load dữ liệu vào bên trong *Activity*

Loaders sử dụng `LoaderManager`ddeer quản lý một hoặc nhiều loaders. `LoaderMananger` bao gồm một tập các callback dành việc khởi tạo loaders. Khi hoàn thành load dữ liệu và khi chúng được reset

## Bắt đầu một loader
Sử dụng `LoaderManager` để quản lý một hoặc nhiều `Loader` instance trong một *Acitivity* . Sử dụng phương thức `initLoader()` để khởi tạo một loader và làm nó hoạt động. Tiêu biểu, bạn có thể làm điều này ở `onCreate()`
```java
getLoaderManager().initLoader(0, null, this);
```
Khi sử dụng *Support Library*, gọ phương thức `getSupportLoaderManager()`
```java
getSupportLaderManager().initLoader(0, null, this);
```

Các tham số sử dụng bên trong `initLoader()`
- Một ID để định danh loader. ID này là bất cứ thứ gì bạn muốn
- Các tham só tùy chọn để cung cấp cho bộ tải tại lúc khởi tạo, trong dạn một *Bundle*. Nếu laoder đã tồn tại, các param này sẽ được ignore
- Triển khai `LoaderCallbacks`, thứ sẽ được `LoaderManager` gọi để báo cáo. Trong trường hợp ở trên, lớp đã triển khai interface `LoaderManager.LoaderCallbacks`, bởi vậy tham số đẩy vào là chính nó

Phương thức `initLoader()` gọi 2 hướng đầu ra có thể
- Nếu như loader ID đã tồn tại, loader cuối cùng được khởi tạo sử dụng ID đó sẽ được tái sử dụng
- Nếu như loader chỉ định bằng ID đó chưa tồn tại, `initLoader()` sẽ khihcs hoạt `onCreateLoader()`. Đây là nơi bạn sẽ implement code để khởi tạo và trả về một loader mới

## Restart loader
Khi `initLoader()` sử dụng một loader đã tồn tại, nó không thay thế dữ liệu và loader đã chứa, nhưng thỉnh thoảng, bạn sẽ muốn làm điều này. Sử dụng `restartLoader()` và pass ID của loader nào mà bạn muốn restart. Điều này sẽ ép loader sử dụng param mới.
- `restartLoader()` sử dụng các tham số giống như `initLoader()`
- `restartLoader()` kích hoạt hàm `onCreateLoader()`, giống như `initLoader()` làm khi khởi tạo loader mới
- Nếu một loader với ID cho trước đã tồn tại, `restartLoader()` sẽ restart định danh của loader và thay thế dữ liệu
- Nếu như chưa tồn tại, `restartLoader()` bắt đầu một loader mới

## LoaderManager callback
`LoaderManager` tự động gọi `onStartLoading()` khi tạo loader. Sau đó, `LoaderManager` quản lý tạng thái của loader dựa vào trạng thái của *Activity* và dữ liệu, ví dụ bằng cách gọi `onLoadFinished()` với dữ liệu đã được load.

Để tương tác với loader, sử dụng một `LoaderManager callback` trong *Activity* khi dữ liệu được cần
- Gọi `onCreateLoader()` để khởi tạo và rtar về một loader mới cho ID
- Gọi `onLoadFinished()` khi loader được khởi tạo trước đó đã hoàn thành load dữ liệu.  Điều này chỉ ra bạn di chuyển dữ liệu vào trong *Activity*
- Gọi `onLoaderReset()` khi loader khởi tạo trước đó bị reset, và làm cho dữ liệu trể nên không khả dụng. Ở trường hợp này bạn nên gỡ thể hiện mà nó có tới dữ liệu của loader

Subclass của `Loader` chịu trách nhiệm dành cho loading data. `Loader` subclass bạn sử dụng phụ thuộc vào kiểu dữ liệu và bạn load, nhưng một trong những các đơn giản nhất là `AsyncTaskLoader`

## AsyncTaskLoader
`AsyncTaskLoader` là trình tải tương đương với `AsyncTask`. `AsyncTaskLoader` cung cấp một phương thức, `loadInBackground()`, chạy trên một luồng riêng biệt. Kết quả của `loadInBackground()` được tự động phục vụ tới UI thread, bằng cách gọi `onLoadFinished()` của `LoaderManager` callback

## AsyncTaskLoader
Để định nghĩa một subclass của `AsyncTaskLoader`, tạo một lớp kết từa `AsyncTaskLoader<D>` , khi D là kiểu dữ liệu màn bạn muốn thực hiện load. Ví dụ `AsyncTaskLoader` dưới đây load danh sách String
```java
public static class StringListLoader extends AsyncTasskLoader<List<String>>{}
```

Tiếp theo, triển khia một constructor phù hợp với lớp cha
- Constructor lấy ngữ cảnh của app như là tham số và đẩy nó vào `super()`
- Nếu loader của bạn cần thêm thông tin để thực hiện load, constructor có thể thêm vào các tham số
Ví dụ
```java
public StringListLoader(Context context, String queryString) {
	super(context);
	mQueryString = queryString;
}
```

Để thực hiện load, sử dụng `loadInBackround()` và viết lại phương thức, hệ quả của phương thức `doInBackground()` của `AsyncTask`
```java
@Override
public List<String> loadInBackgournd() {
	List<String> data = new ArrayList<String>;
	return data;
}
```

