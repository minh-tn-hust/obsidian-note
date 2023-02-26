## Khai bán quyền sử dụng internet
```xml
<manifest>
	<uses-permission android:name="android.permission.INTERNET"/>
</manifest>
```

Để thực hiện lắng nghe trạng thái các kết nối mạng, sử dụng quyền
```xml
<manifest>
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
</manifest>
```

## Thực hiện các hoạt động mạng trong một luồng công nhân
Luôn luôn thực hiện các thao tác mạng trên các luồng công nhân, riêng rẽ với luồng UI. Ví dụ, trong Java code của bạn có khởi tạo một `AsyncTassk` trinber khai việc mở một kết nối mạng và truy vấn API. Code chúng của bạn phải chết nếu như mà kết nối mạng được hoạt động. Nếu vậy, nó sẽ chạy AsyncTassk trong một luồng riêng biệt, sau đó hiển thị kết quả lên UI

## Tạo một kết nối HTTP
Hâu hét các kết nối mạng trên Andoird App sử dụng HTTP và HTTPS để gửi và nhận dữ liệu thống qua mạn

`HTTPConnection` hỗ trợ hầu hết các tính năng kết nối mạng hiện nay bao gồm: HTTPS, upload và download file, IPv6, ...

## Xây dựng URI
Để mở một HTTP kết nối, bạn cần xây dựng một yêu cầu URI như là một đối tượng *Uri*. Để cấu tạo một URI request, sử dụng `URI.parse()` với phương thức `buildUpon()` và `appendQueryParameter()`. Xem code dưới đây
```java
final String BOOK_BASE_URL = "https://www.gooleapis.com/books/vi/volumes?";

final String QUERY_PARAM = "q";
final String MAX_RESULTS = "maxResults";
final String PRINT_TYPE = "printType";


Uril builtURI = Uri.parse(BOOK_BASE_URL).buildUpon().appendQueryParameter(QUERY_PARAM, "pride+prejudice").appendQueryParameter(MAX_RESULTS, "5").appendQueryParameter(PRINT_TYPE, "books").build();
```

## Kết nối và download dữ liệu
Luồng công nhân thực hiện các giao dịch mạng, ví dụ bên trong hàm `doInBackground()` trong `AsyncTask`, sử dụng `HttpURLConnection` để thực hiện HTTP Get và download dữ liệu về. Cách để làm
1. Để có được một `HttpURLConnection`, gọi `URL.openConnection()` sử dụng URI mà bạn đã xâu dựng. Ép kiểu kết quả thành HttpURLConnection()
2. Thiets lập các tham số tùy chọn. Dành cho kết nối chậm, bạn muốn có thời gian timeout dài hoặc timeout đọc. Để thay đổi phương thức request `GET`, sử dụng `setRequestMethod()`. Nếu không muốn sử dụng mạng cho đầu vào, gọi hàm `setDoInput()` với tham số là `false`
4. Mở một dòng đọc sử dụng `getInputStream()`, sau đó đọc kết quả trả về và chuyển nó thành string. Header trả về bao gồm các thông tin thêm như là loại nội dung của phản hồi và độ dài, ngày hỉnh sửa và cookies phiên. Nếu như phản hồi không có body, `getInputStream()` trả về một dòng trống
5. Gọi `disconnect()` để đóng kết nối. Disconnect giải phóng tài nguyên được tổ chức của một kết nối và chúng có thể đóng hoặc sử dụng lại


## Uploading dữ liệu
Nếu như bạn đang đẩy dữ liệu lên một web server, bạn cần upload một request body, thứ mà giữ dữ liệu được gửi lên. Để làm điều này
1. Cài đặt kết nối mà đầu ra có thể sử dụng bằng cách gọi `setDoOutPut(true)`. Mặc định, `HttpURLConnection` sử dụng HTTP `GET`. Khi `setDoOutput` được đặt true, `HttpURLConnection` sử dụng HTTP `POST`
2. Mở một dòng đọc bằng cách gọi `getOutputStream()`

## Ví dụ
```java
private String downloadUrrl(String myUrl) throws IOException {
	InputStream inputStream = null;
	int len = 500;
	try {
		URL url = new URL(myUrl);
		HttpURLConnection conn = (HttpURLConnection) url.openConnection();
		conn.setReadTimeout(10000 /* miliseconds */);
		conn.setConnectTimeout(15000 /* miliseconds */)
		conn.connect();
		int response = conn.getResponseCode();
		Log.d(DEBUG_TAG, "The response is: " + response);
		inputStream = conn.getInputStream();

		String contentAsString = convertInputToString(inputStream, len);
		return contentAsString;
	} finally {
		conn.disconnect();
		if (inputStream != null) {
			inputStream.close();
		}
	}
}
```

## Chuyển đổi InputStream sang string
Một `InputStream` là một nguồn các byte có thể đọc được. Khi bạn nhận được `InputStream`, thuông thường sẽ giải mã và chuyển nó thành loại dữ liệu mà bạn muốn. Trong trường hợp trên, `InputStreamm` biểu diễn một đoạn text 

Phương thức `convertInputToString()` định nghĩa bên dưới chuyển `InputStream` sang một chuỗi mà *Activity* có thể hiện thị nó lên UI. Phương thức sử dụng một instance của `InputStreamReader` để đọc byte và giải mã chúng thành các kí tự
```java
public String convertInputToString(Input Streamstream, int len) throws IOException, UnsupportedEncodingException {
	Reader reader = null;
	reader = new InputStreamReader(stream, "UTF-8");
	char[] buffer = new char[len];
	reader.read(buffer);
	return new String(buffer);
}
```

## Chuyển đổi kết quả
Khi bạn tạo một truy vấn tới web API, kết quả trả về thường ở dạng JSON
Để tìm quá trị của một item trong kết quả phản hồi, sử dụng phương thức từ các lớp `JSONObject` và `JSONArray`. Ví dụ, dưới dây là các để tìm giá trị `"onclick"` giá trị của item thứ 3 trong mảng `menuitem`:
```java
JSONObject data = new JSONObject(responseString);
JSONArray menuItemArray = data.getJSONArray("menuitem");
JSONObject thirdItem = menuItemArray.getJSONObject(2);
String onClick = thirdItem.getString("onclick");
```

## Quản lý trạng thái mạng
Tạo kết nối mạng thường đắt đỏ và chậm, cụ thể nếu thiết bị có ít khả năng kết nối. Cẩn thận về trạng thái kết nối mạng sẽ ngăn cản app của bạn từ thử tới tạo các kết nối mạng khi mạng không có sẵn

Đôi khi máy bạn cũng cần thiết biết kết nối mạng hiện tại là gì, mạng Wifi hay là dữ liệu di động, để có thể điều hướng các task. Ví dụ, bạn muốn đợi cho tới khi kết nối là kết nối Wifi để thực hiện download file

Để check kết nối mạng, sử dụng các lớp sau
- `ConnectivityManager` trả lời các truy vấn về trạng thái kết nối mạng. Nó cũng thông báo các app khi kết nối mạng bị thay đổi
- `NetworkInfo` miêu thả trạng thái của một cổng mạng của type cho trước (kết nối hiện tại hoặc mobile hoặc Wifi).

```java
private static final String DEBUG_TAG = "NetworkStatusExample";
ConnectivityManager connMgr = (ConnectivityManager) getSystemService(Context.CONNECTIVITY_SERVICE);
NetworkInfo networkInfo = connMgr.getNetworkInfo(ConnectivityManager.TYPE_WFIFI);
boolean isWifiConn = networkInfo.isConnected();
networkInfo = connMgr.getNetworkInfo(ConnectivityManager.TYPE_MOBILE);
Log.d(DEBUG_TAG, "Wifi connected: " + isWifiConn);
Log.d(DEBUG_TAG, "Mobile connected: " + isMobileConn);
```

Đoạn code trên kiểm tra xem Wifi và mobile có được kết nối
- `getSystemService()`A lấy một instance của `ConnectivityManagerA`A từ ngữ cảnh hiện tại
- `getNetworkdInfo()` lấy trạng thái kết nối Wifi của thiết bị, sau đó là kết nối mobile. Phương thức này trả về một đối tượng `NetworkInfo`, chứa thông tin về trạng thái mạng được cho trước
- Phương thức `networkInfo.isConnected()` trả về true nếu như mạng đang được kết nối. Nếu như mạng đang được kết nối, nó có thể sử dụng để thiết lấp socket  và thực hiện truyền dữ liệu

