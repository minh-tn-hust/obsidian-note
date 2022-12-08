# Giới thiệu
Trong Part 1, chúng ta đã thấy cách mà Redux giúp chúng ta build app một cách có thể duy trì được bằng cách cho chúng ta một vị trí trung tâm và bỏ global state vào. Chúng ta cũng nói về các khái niệm core Redux như là dispatching action object, sử dụng các hàm reducer để trả về new state và viết logic bất đồng bộ sử dụng thunks. Trong part 2, chúng ta đã thấy các API như configureStore và createSlice hoạt động như thế nào. Từ Redux Toolkit và Provider và useSelector từ React-Redux làm việc với nhau để cho phép chúng ta viets Redux logic và tương tác cùng với các logic tới từ các React component

Hiện tại bạn đã có một vài ý tưởng về những thứ này là gì, đây là thời gian để chúng ta đẩy kiến thức vào thực hành. Cúng ta sẽ build một app bảng tin media nhỏ, sẽ bao gồm một vài tính nắng để trình diễn một vài usecaese trong thực tế. Thứ này sẽ giúp chúng ta hiểu cách sử dụng Redux trong các ứng dụng

## Project Setup
Với tutorial này, chúng ta cần tạo một projcet được config sẵn  và đã được cài React + Redux, bao gồm một vài style mặc định, và có một FAKE API cho phép chúng ta viết API thực vào bên trong APP. Bạn sẽ sử dụng cái này như là cơ bản dành cho việc viết code ứng dụng thực tế
[Github repo](https://github.com/reduxjs/redux-essentials-example-app)


### Tạo một Redux + React Project
Khi bạn đã hoàn thành xong tutor này, bạn có lẽ sẽ muốn thử làm việc với chính project của bạn. Chúng tôi khuyển khích bạn sử dụng [Redux Template dành cho Create-React-App](https://github.com/reduxjs/cra-template-redux) như là cách nhanh nhất để có thể tạo ra một Redux + React project mới. Nó tới từ Redux Toolkit và React-Redux đã được config sẵn, sử dụng ví dụ app counter như bạn thấy trong Part 1. Việt này giúp bạn nhảy vào đúng chỗ để viết code luôn mà không cần phải ad thêm Redux packages và cài đặt store

### Khám phá Project khởi tạo
Xem qua thử xem project chứa những gì


