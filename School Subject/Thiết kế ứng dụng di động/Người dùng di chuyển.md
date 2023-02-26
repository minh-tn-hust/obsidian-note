Có thể sử dụng các loại *Navigation* sau để người dùng có thể điều hướng bên trong App
- Back navigation, người dùng sử dụng để điều hướng về màn hình trước sử dụng nút *Back*
- Phân cấp navigation, người dùng điều hướng thông qua một hệ thông phân cấp màn hình. Hệ thống phân cấp được tổ chức với một màn hình cha và tập các màn hình con

## Mẫu phân cấp Navigation
![App screen hierarchy](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/4-4-c-user-navigation/dg_app_hierarchy.png "App screen hierarchy")
Một ứng dụng được tổ chức trong một hệ thống phân cấp cha-con
## Màn hinh cha
Một màn hình cha (ví dụ như màn hình home screen của app) có kả năng điều hướng xuống các màn hình con
- *Activity* chính của app thường là màn hình cha
- Triển khai một màn hình cha như là một *Activity* với các điều hướng xuống một hoặc nhiều màn hình con

## Màn hình anh em
Các anh em là các màn hình ở cùng vị trí trong hệ thống phân cấp, được chia sẻ chung màn hình cha
- Ở level đầu tiên, các màn hình con có thể là tập các màn hình chứa các headline
- Triển khai màn hình con như là *Activity* haowcj là *Fragment*
- Triển khai điều hướng bên để có thể điều hướng từ một anh em sang một anh em sáng trong cùng một level
- Nếu có các màn hình level thứ 2, màn hình level thứ nhất là cha của các màn hình level 2. Triển khai điều hướng con cháu tới các màn hình con level 2


# Back-button
Nếu trong hệ thống phân cấp màn hình, người dùng đang ở tầng thứ nhất của các con, thì khi người dùng sử dụng back-button, Android sẽ đưa người dùng về với màn hình con trước đó
# Up-button
Nếu trong hệ thống phân cấp màn hình, người dùng đang ở tầng thứ nhất của các con, thì khi người dùng sử dụng up-button, Android sẽ đưa người dùng về với màn hình cha chứ không phải là màn hình con xem ở trước đó
Để cung cấp Up button màn màn hình con, khai báo cha của *Activity* trở thành *Activity* chính trong AndroidManifest.xml
```xml
<activity android:name="com.example.android.droidcafeinput.OrderActivity"
    android:label="Order Activity"
    android:parentActivityName=".MainActivity">
    <meta-data android:name="android.support.PARENT_ACTIVITY"
        android:value=".MainActivity"/>
</activity>
```

Đoạn code trên khai báo cha mẹ của màn hình con *OrderActivity* là *MainActivity*. Nó cũng set luôn *android:label* thành tiêu đề của màn hình *Acitivity* thành "Order Activity". Màn hình con bây giờ đã bao gồm cả *Up* button trên thanh App bar, người dugnf có thể thực hiện điều hướng về màn hình Cha

## Điều hướng con cháu
Với điều hướng con cháu, bạn cho phép người dùng đi từ màn hình cha tới các màn hình con ở level đầu tiên. Và từ các màn hình cấp độ 1, có thể đi xuống các màn hình cấp độ 2.
![Descendant navigation](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/4-4-c-user-navigation/dg_app_hierarchy_descendent_navigation.png "Descendant navigation")

## Các nút bấm và các mục tiêu
Các tốt nhất để điều hướng con xuống con cháu từ màn hình cha tới tập các anh em là sử dụng nút bấm hoặc các mục tiêu đơn giản như các hình ảnh sắp xếp theo thứ tự ... Khi người udngf chạm vào một nút, tập các màn hình con mở ra và thay thế màn hình hiện tại

## Điều hướng drawer
Điều hướng drawer là một bảng thướng được hiển thị các lựa chọn điều hướng ở cạnh bên trái của màn hình
![A navigation drawer](https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/images/4-4-c-user-navigation/dg_nav_drawer_composite.png "A navigation drawer")
## Các để tạo ra Drawer 
DDeer tạo ra layout điều hướng drawer, sử dụng DrawerLayout API có sẵn trong Support Library. 
Để thêm navigation drawer, sử dụng DrawerLayout như là root của ViewGroupo của *Acitivyt*. Bên trong *DrawerLayout*, thêm một *View* chứa nội dung chính của màn hình và một *View* khác, tiêu biểu là một *NavigationView*, chứ nội dung của điều hướng drawer
```xml
<android.support.v4.widget.DrawerLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="true"
    tools:openDrawer="start">

    <include
        layout="@layout/app_bar_main"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

    <android.support.design.widget.NavigationView
        android:id="@+id/nav_view"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        android:fitsSystemWindows="true"
        app:headerLayout="@layout/nav_header_main"
        app:menu="@menu/activity_main_drawer" />

</android.support.v4.widget.DrawerLayout>
```

# Điều hướng người dùng
## Điều hướng cha xuống con
## Điều hướng con lên cha
Cả hai loại điều hướng này khá dễ để triển khai trên *Activity* khi chỉ cần định nghĩa mối quan hệ cha con của các *Acitivity* trong file AndroidManifest.xml. Sau đó sử dụng *Intent* để bật tắt

Đối với điều hướng từ cha lên con, sử dụng *Up* button
Config activity như sau để thể hiện mối quan hệ cha con
```xml
<activity android:name=".OrderActivity"
   android:label="@string/title_activity_order"
   android:parentActivityName=
                        "com.example.android.droidcafe.MainActivity">
   <meta-data
      android:name="android.support.PARENT_ACTIVITY"
      android:value=".MainActivity"/>
</activity>
```
## Điều hướng các anh em cùng cha
Sử dụng Tab, các tab có trên thanh App bar và người dùng có thể thực hiện swipe để di chuyển qua lại giữa các anh em với nhau. Sử dụng Fragment để thực hiện hiển thị các UI. Nó gioogns như một *Mini-Activity*, và có vòng đời riêng.
Triển khai tab theo các bước sau
1. Định nghĩa tab layout. Class chính sử dụng để hiển thị tab là *TabLayout*. Nó cung cấp layout đứng để hiển thị tab
2. Triển khác một Fragment dành cho mỗi màn hình tab
3. Thêm page adapter. Sử dụng lớp *PagerAdapter* để điền "page" vào trong một *ViewPager*, là một quản lý layout cho phép người dùng có thể lập trái hoặc phải thông qua màn hình. Triêng khai *PagerAdapter* để sinh các màn hình mà *View* hiển thị.
4. Tạo instance tablayout, và thêm xâu cho mỗi tab
5. Sử dụng *PagerAdapter* để quản lý màn hình. Mỗi màn hình được biểu diễn bởi một Fragement
Các adapter tiêu chuaaar sử dụng Fragment với ViewPager:
- FragmentPagerAdapter: Được thiets kế danh cho di chuiyener qua lại giữa các màn hình con ae, biểu diễn cứng số lượng nhỏ các màn hình
- FragmentStatePagerAdappter: Được thiết kế dành cho di chuyển qua lại giữa tập các màn hình mà số lượng mà hình không thể quyết định được. Nó phá hủy các Fragment theo điều hướng ủa người dùng. tối ưu bộ nhớ sử dụng
## Điều hướng Drawer