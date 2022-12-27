**AndroidManifest.xml** -> file cần thiết để hệ thống Android có thể chạy được, tất cả cá thành phần có trong một App, ví dụ như mỗi Activity phải được khai báo trong file XML này.

**Activity** là màn hình hiển thị lên cho người dùng thấy

Add log vào trong code để hiển thị tin nhắn: 
```java
Log.d("MainActivity", "Hello World");
```
Trong đó
- **Log** : Log class sử dụng để gửi log message tới Logcat pane
- **d** : Debug Log, cài đặt để có thể lọc được các message bên cạnh đó còn có e (Error), w (Warn), i (Info)
- **"MainActivity"** : biến số đầu tiên như là một cái tag sử dụng để có thể lọc được message ở trong Logcat panel
- **"Hello world"** : biến số thứ 2 như là message thực sự

**build.gradle** : sử dụng để khi cần thêm các thư viện mới vào trong project
**AndroidManifest.xml** : thêm tính năng, các thành phần và các quyền cho Android app



## Folder java
Chứa các file Java. Mỗi **Activity**, **Service** hoặc là một thành phần (ví dụ như **Fragment**) đều được định nghĩa như là một Java class

## Layout files
Để xem và chỉnh sửa một layout file, mở folder **res**, vào folder **layout**, ở ví dụ trên, đối với MainActivity.java có file layout là activity_main.xml

# Resource file
Folder **res** chứ các resources ví dụ như layouts, string, images. Một **Activity** luôn luôn có quan hệ với layout của một UI được định nghĩa bằng các file XML. File XML này thường được đăt tên phía sau Activity. Thư mục **res** chứ các thư mục con sau:
- **drawable** : Chứa các ảnh có bên trong app
- **layout** : Với mỗi **Activity** có ít nhất một file layout viết bằng XML để có thể miêu tả UI
- **mipmap** : Sử dụng để có thể chứa icon khởi tạo của App. Trong này có một thư mục con dành cho mỗi mật độ điểm ảnh được hỗ trợ. Android sử dụng mật độ điểm ảnh để có thể quyết định độ phân giải cần thiết của hình ảnh
- **values** : thư mục này chứa các định nghĩa về string, màu, các miền để tránh hardcode bên trong file XML và file Java
	- colors.xml : sử dụng để định nghĩa các màu cần thiết
	- demens.xml : sử dụng để định nghĩa các size của view và các đối tượng dành cho các đọ phân giải khác nhau
	- strings.xml : sử dụng để làm localize
	- styles.xml : Theme và styles của map đều đến từ đây. Styles giúp app có thể trông thống nhất hơn với tất cả các thành phần Ui


# Android manifest
Trước khi hệ thống Android có thể bắt đầu các thành phần của App như là một Activity, hệ thống phải biết được các Activitiy đang tồn tại. Làm được việc đó bằng cách đọc file Android Manifest.xml của app, cái này sẽ mô tả các thành phần của một app Android. Mỗi Activity pahri được liệ kê trong file XML này cùng với các thành phần dành cho App\


# Các layout và resource dành cho UI
## Views
UI bao gồm một hệ thống phân cấp các đối tượng gọi là views - mỗi thành phần của màn hình là một **View**. Lớp **View** biển diễn cho một khối xây dựng cơ bản cho tất cả các thành phần UI, và lớp cơ sở cho các class cung cấp các thành phần UI tương tác như là button, checkboxes và text

# ViewGroup groups
Các thành phần **View** được nhóm lại bên trong một ViewGroup, thứ mà hoạt động như là một container. Mối quan hệ giữa chúng là cha-con, trong đó cha là ViewGroup và con là View và các ViewGroup khác. 

# Bố cục nhóm các ViewGroup
Các thành phần **View** dành cho một màn hình được tổ chức thành một hệ thống phân cấp. Tại rôt của hệ thống phân cấp này là một **ViewGroup** chứa bố cục của toàn bộ màn hình. **ViewGroup** này chứ các thành phần View con và nhưng **ViewGroup** khác như hình được show dưới đây![[Pasted image 20221227214042.png]]

Một vài **ViewGroup** được thiết kế như là bố cục bởi vì chúng tổ chức các thành phần View con theo một các riêng và thường được sử dụng làm **ViewGroup** gốc

## Sử dụng ConstraintLayout
Một *constraint* là một kết nối / một sự điều chỉnh tới thành phần UI khcs, tới parent của bố cục haowcj là một hướng dẫn vô hình. Mỗi constraint xuất hiện như là một dòng mởi trộng từ một tay nắm tròn
- **Baseline Constraint** : căn chỉnh một thành phần UI chứa text chẳng hạn như **TextView** hoặc là **Button** với một thành phần UI khác có chứa text. Một *baseline constraint* cho phép bạn constraint các thành phần để từ đó text baseline match được với nhau
- match_constraint : sử dụng để fill hết toàn bộ bố mẹ cho tới lề (nếu như lề được set)
- wrap_content : thu nhỏ thành phần UI bằng với kích thước của nội chung chứa bên trong nó, nếu như không có nội dung -> không thể nhìn thấy
- Sự dụng số cự thể nếu như muốn set chiều dài / rộng

```xml
android:id="@+id/button_count" 
sử dụng để định danh một thành phần View nào đó
sử dụng dấu + để biểu thị răng bạn tạo mới một id
bỏ dấu + đi khi muốn refer đến một View nào đó
```

## Sử dụng LinearLayout
>Là một layout tuyến tính giống như Row và Column
>LineaerLayout yêu cầu các thuộc tính sau phải được set
>- android:layout_width : chiều rộng
>- android:layout_height : chiều dài
>- android:orientation : hướng của layout
>- android:layout_gravity : quyết định cách sắp xếp các thành phần so với bố mẹ của nó
>- android:padding
>- andoird:padding(T/B/L/R)
>- android:paddingStart : Padding ở cạnh bắt đầu của View
>- android:paddingEnd : Padding ở cạnh kết thúc của View


## Sử dụng RelativeLayout
>Layout này làm cho các con của nó có mối quan hệ với nhau, sử dụng một element khác để làm mốc thiết lập vị trí cho một element mới, các thuộc tính mà các con ở bên trong RelativeLayout có thể có
>- android:layout_toLeftOf : bên trái của một bên cách bên phải của một bên khác
>- android:layout_toRightOf : bên phải của một bên so với bên trái của một bên khác
>- android:layout_centerHorizontal : căn giữa theo chiều ngang của bố mẹ
>- android:layout_centerVertical : căn giữa theo chiều dọc của bố mẹ
>- android:layout_alignParentTop : căn theo top của bố mẹ
>- android:layout_alignParentBottom : căn theo bottom của bố mẹ

## TextView
>Sử dụng để hiển thị text lên màn hình
>Các thuộc tính có thể
>android:text : sử dụng để set text hiển thị
>android:textColor : sử dụng để set màu hiển thị text
>android:textAppearance : sử dụng để link tới một resource khác
>android:textSize : sử dụng để set text size (đơn vị là sp - scaled-pixel)
>android:typeface : sử dụng để set kiểu chữ
>android:lineSpacingExtra : sử dụng để set khoảng cách giữa các dòng text
>android:autoLink : sử dụng để điều kiển text như là một link url / email


## ScrollView
Class cung cấp bố cục cho các view scroll theo chiều dọc, là một lớp con của FrameLayout
Tất cả nội dung của một ScrollView chiếm bộ nhớ kể cả khi vị trí của chúng có được hiển thị hay không. Điều này làm cho **ScrollView** hữu dụng cho các page muốn scroll mượt và có text bởi vì text đã rẵn sàng ở trong bộ nhớ. Tuy nhiên ScrollView với một ViewGroup có chứa nhiều thành phần View sẽ chiếm nhiều bộ nhớ, có thể ảnh hưởng tới hiệu năng của toàn bộ app


## Activity
Một *activity* biểu diễn cho một màn hình riêng lẻ trong app với giao diện người dùng có thể tương tác được. 
Mỗi khi một *activity* mới được bắt đầu, *activity* trước đó sẽ bị dừng tại, nhưng hệ thống giữ hoạt đọng đó trong một stack. Khi người dùng xong với hoạt động hiện tại và bâm snuts quay lại, họt động sẽ được lấy ra từ stack và hủy, và hoạt động trước đó sẽ được tiếp tục

Khi một *activity* bị dừng lại bởi vì một hoạt động moiwst bát đầu, hoạt động đầu tiên được thông báo bắng các lifecycle method - tập các trạng thái của một *Activity* có thể tồn tại : khi một hoạt động được khởi tạo lần đầu tiên, khi chúng dừng, khi chún dược tiếp tục và khi cả hệ thống bị phá hủy

### Tạo Activity trong App
> - Tạo một Activity Java class
> - Triển khai UI của Activity trong một file layout XML
> - Định nghĩa hoạt động mới bên trong AndroidManifest.xml
> - Triển khai các phương thức vòng đời cần thiết và cái quan trọng nhất là **onCreate()**
> - Bên trong **onCreate()** có gọi tới **setContentView()** để thực hiện khởi tạo layout UI 

#### Lưu ý khi mới khởi tạo Activity
Khi bạn tạo một project mới trong Android Studio và chọn Backwards Compatibility, MainActivity được mặc định , đó là một lớp của AppCompatActivity. Lớp AppCompatActivity cho phép bạn sử dụng các tính năng mới nhất của Andrỏid như là app bar và Material Design trong khi vẫn có khả năng máy của bạn tương thích với các thiết bị chạy các Android version cũ hơn

Nhiệm vụ đầu tiên của bạn trong một lớp con *Activity* là triển khai phương thức vòng đời tiêu chuẩn để có thể handle được các trạng thái thay đổi với *Activity* của bạn. Những trạng thái thay đổi này bao gồm những thứ ví dụ như khi *Activity* được khởi tạo, dùng lại, tiếp tục và phá hủy

Một callback yêu cầu mà app của bạn bắt buộc phải triển khai đó là phương thức onCreate(). Hệ thống gọi method này khi nó khởi tạo *Activity* của bạn và tất cả các thành phần quan trong trong *Activity* của bạn đều được khởi tạo ở đây. Quan trong nhất, phương thức *onCreate()* gọi *setContentView()* để khởi tạo layout tiêu chuẩn cho *Activity*

#### Layout và Activity

Bạn thường định nghĩa UI dành cho *Activity* trong một hoặc nhiều file bố cục XML. Khi phương thức **setContentView()**  được gọi với đường dẫn tới một file layout, hệ thống tạo ra tất cả các view ban đầu từ các layout riêng biệt và thêm chúng vào *Activity* của bạn. Như này thường được gọi là inflating layout

### Triển khai hoạt động của UI
UI dành cho một UI cung câp một hệ thống phân câp các thành phần View, thú điều khiển một khoảng không gian cụ thể bên trong cửa sổ activity và có thể phản hồi với tương tác của người dùng.

Các thông thường nhất để định nghĩa một UI sử dụng thành phần View là: với một file bố cục XML lưu trữ như là một phần tài nguyên app của bạn. Định nghĩa bố cục của ban trong XML cho phép bạn có thể duy trì thiết kế của UI độc lập với source code - nơi định nghĩa các hành vi của *Activity*

### Khai báo Activity trong AndroidManifest.xml
Với mỗi Activity trong app của bạnh phải được khởi tạo ở trong Androidmanifest.xml với thành phần <activity>, bên trong khu <application>. Khi bạn tạo một project mới haowcj thêm ột hoạt động mới vào project trong Android Studio, AndroidManifest.xml đưuọc tạo hoặc update để bao gồm khung khởi tạo cho mỗi Activity. Dưới đây một khai bào dành cho MainActivity 

