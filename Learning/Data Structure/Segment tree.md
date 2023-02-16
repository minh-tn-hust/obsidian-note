Segment Tree là một cấu trúc dữ liệu mà lưu trữ thông tin về một khoảng mảng (array interval) như làm một cái cây. Điều này cho phép trả lời các cấu truy vấn trên một khoảng trên toàn bộ mảng một cách hiệu quả, trong khi vẫn có đủ thời gian để cho phép thay đổi nhanh bên trong mảng. Điều này bao gồm tìm tổng của các phần tử liên tiếp trong mảng a[l...r] hoặc là tìm phần tử nhỏ nhất trong một khoảng nhất định trong độ phức tạp O(log n). Giữa việc trả lời các câu truy vấn, ST cho phép thay đổi mảng bằng cách thay thế một phần tử, hoặc thấm chí thay đổi nhiều phần tử của cả một chuỗi con (định nghĩa tất cả phần tử trong khoảng L -> R bằng bất cứ giá trị nào, hoặc là thêm một giá trị vào tất cả các phàn tử có trong chuỗi con)

Thông thường, một ST là một cấu trúc dữ liệu rất đa năng, và một lượng lướng các vấn đề có thể giải quyết với nó. Thêm vào đí. nó cũng có khả năng ứng dụng các toán tử phức tạp hơn và trả lời các câu truy vấn phức tạp xem [Phiên bản nâng cao của ST](https://cp-algorithms.com/data_structures/segment_tree.html#advanced-versions-of-segment-trees) . Trong tính huống cụ thể, ST ó thể dễ dàng chuẩn hóa tới các trường lớn hơn. Cụ thể, với một ST 2 chiều, bạn có thể trả lời các truy vấn tổng/nhỏ nhất qua một số các hình chữ nhất con của một ma trận cho trước chỉ trong O(log n * log n)

Một tính chất quan trọng của ST là chúng chỉ yêu cầu một lượng bộ nhớ tuyến tính. Tiêu chuẩn của ST yêu cầu 4n đỉnh dành cho việc lưu trữ một mảng có chiều dài là n

# Dạng đơn giản nhất của Segment Tree
Để bắt đàu một cách đơn giản, chúng ta sẽ xem xét qua dạng đợn giản nhất của một ST. Chúng ta muốn trả lời cũng truy vấn về tổng một cách hiệu quả. Định nghĩa rõ ràng về nhiệm vụ của chúng ta là: Cho một cái mảng a[0 ... n - 1], ST phải có khả năng tìm được tổng của các phần tử nằm giữa vị trí L và R (tổng từ l đến r) và cũng có thể thực hiện thay đổi gia trị của các phần tử trong mảng (biểu diễn nhiệm vụ dạng a[i] = x). ST có khả năng xử lý cả 2 truy vấn trong O(log n)

Đây là một sự cải tiến so với các phương pháp đơn giản hơn. Triển khai một mảng thuần - chỉ sử dụng mảng đơn giản - có thể cập nhật phần tử trong O(1) nhưng truy vấn yêu cầu O(n) để có thẻ tính toán mỗi truy vấn tính tổng. Và việc tính trước prefix sum có thể tính toán O(1) nhưng khi update các phần tử trong mảng laijyeeu cầu O(n) để thay đổi prefix sum

# Cấu trúc của ST
Chúng ta có thể áp dụng giải pháp chia để trị khí nói đến các phân đoạn của mạng. Chúng ta tính toán và lưu trữ tổng của các phần tử trong cả một mảng, nói cách khác tổng của phân đoạn a[0...n-1]. Sau đó chúng ta chia mảng hành 2 nửa a[0...n/2 - 1] và a[n/2...n-1] và tính toán tổng của mỗi nữa và lưu chúng lại. Mỗi nửa của 2 nửa này được chia ra thành các nửa, và cứ làm thể cho tới khi tất cả các phân đoạn đạt được độ lớn bằng 1

Chugns ta có thể xem các phân đoạn này như là dạng của một cây nhị phân: root của cây này là phân đoạn từ 0 -> n-1, với mỗi đỉnh (ngoại trừ các đỉnh lá) có chính xác 2 đỉnh con. Đây là lý do tại sao lại gọi cấu trúc dữ liệu này là ST, thậm chiis trong hầu hết các triển khai của cây không được cấu trúc một cách tường mình. Dưới đây là biểu diễn về một ST với mảng a = [1, 3, -2, 8, -7]
!["Sum Segment Tree"](https://cp-algorithms.com/data_structures/sum-segment-tree.png)

Từ miêu tả ngắn về cấu trúc dữ liệu, chúng ta có thể kết luận rằng một ST chỉ yêu cầu số lượng tuyến tính các đỉnh. Tại tầng đầu tiên của cây chứa một node đơn (root node), tầng thứ 2 chứa 2 đỉnh, và tại tầng thứ 3 chứa 4 đỉnh, chơi tới khi số lượng các đỉnh chạm tới n. Bởi vậy số lượng các đỉnh trong trường hợp xấu nhất có thể ước lượng bằng tổng của 1 + 2 + 4 + ... + 2^(log2 n) < 2(log2 n + 1) < 4n

Nhớ rằng, khi mà n không phải là lũy thừa của 2, không phải tất cả các tầng của ST được đầy đủ. Chúng ta có thể thấy hành vi đó ở ảnh trên. Và bây giờ chúng ta có thể quên đi về sự thật này, nhưng nó cũng trở nên quan trọng trong suốt quá trình triển khai

Chiều cao của ST là O(log n), bởi vì khi đi xuống từ gốc cho tới lá, kích thước của các phân đoạn giảm đi xấp xỉ một nửa

# Cấu tạo
Trước khi cấu trúc một ST, chúng ta cần quyết định
1. Giá trị lưu tại mỗi node của ST. Ví dụ, ở trong ST tổng, một node lưu trữ tổng của các phần trong đoạn [l, r]
2. Toán tử merge thực hiện hợp 2 anh chị em trong một cây nhị phân. Ví dụ, trong cây nhị phân tổng, 2 node tương ứng là a[l1...r1] và a[l2...r2] có thể được hợp lại vào một node tương ứng tới a[l1...r2] bằng cách thêm giá trị của 2 node

Lưu ý rằng, một đỉnh là một đỉnh lá nếu như nó tương ứng với phân đoạn và chỉ bao phủ một giá trị trong mảng ban đầu. Nó biểu diễn tầng thấp nhất của ST. Giá trị của nó có thể bằng (tương ứng) so với phần tử a[i]

Bây giờ, dành cho việc cấu tạo ST, chúng ta bắt đầu từ level bên dưới (các đỉnh lá) và khai báo chúng các giá trị tương ứng. Cơ bản về những giá trị này, chung ta có thể tính toán giá trị của các level trước bằng cách sử dụng toán từ merge. Cơ bản, chúng ta có thể tính toán được các giá trị ở phía trước, và lập tại thủ túc cho tới khi chúng ta tới được node gốc

Thuận tiện để miêu tả toán tử này 