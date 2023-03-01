# Kiểm thử luồng điều khiển
## Xây dựng đồ thị luồng điều khiển
>- Biểu diễn đồ thị cấu trúc của một chương trình
>- Chuỗ các câu lệnh từ điểm đầu tới điểm kết thúc của các đơn vị được mô tả sử dụng khái niệm đồ thị

## Lựa chọn các đường dẫn liên quan dựa trên một số tiêu chí
#### All paths: tất cả các đường
>Thiết kế tất cả các test case có thể có, nhờ vậy mà tất cả các đường dẫn của chương trình đều được thực thi
#### Statement Coverage: Bao phủ câu lệnh
>Thực thi mỗi câu lệnh ít nhất một lần

#### Branch Coverage: Bao phủ nhánh
>Một nhánh là một cạnh đường ra từ một node
>- Một note hình chữ nhật có nhiều nhất một nhánh đi ra
>- Một note hình thoi có 2 nhánh đi ra
>Lựa chọn các đường dẫn mà mỗi nhánh được bao bọc ít nhất trong một đường dẫn



# Predicate Coverage: Bao phủ điều kiện
>- Predicate: là một biểu thức có thể được đánh giá bằng các giá trị true hoặc false
>- Cấu trúc bên trong được tạo bởi các toán tử logic
>	- And
>	- Or
>	- Xor
>	- Not
>- Mệnh đề: là một điều kiện mà không chứa bất kì toán tử logic nào


## Bao phủ điều kiện (PC)
- Đảm bảo tất cả các điều kiện trong source được triển khai đúng
- Với mỗi điều kiện p, test case phải thỏa mản răng p được đánh giá true ít nhất một lần và p được đánh giá false ít nhất một lần

## Bao phủ mệnh đề (CC)
- Với mỗi điều kiện cụ thể (mệnh đề) c, c nên được đánh giá bằng true và đánh giá bằng false ít nhất một lần

## Bao phủ kết hợp (CoC)
- Với mỗi điều kiện p, test case nên đảm bảo rằng các mệnh đề trong p nên được đánh giá với mỗi tổ hợp có thể có của các giá trị đúng
- Yêu cầu tất cả các tổ hộp có thể có

## Mệnh đê chủ động (AC)
- Mệnh đề chủ động: là mệnh đề được tâp trung vào
- Mện đề phụ: tất các các mệnh đề khác trong điều kiện
- Một mệnh đề ci trong điều kiện p, gọi là mệnh đề chính, quyết định p khi và chỉ khi giá trị của các mệnh đề phụ cj không ảnh hưởng và chỉ ci thay đổi khiến p thay đổi

## Bao phủ mệnh đề chính (ACC)
>Với mỗi điều kiện p, với mỗi mệnh đề chính c thuộc p, chọn các mệnh đề phụ để cho c quyết định p. Yêu cầu 2 test case, c đánh giá là true và c đánh giá là false

## GACC
>- Với mỗi mệnh đề c, chọn các mệnh đề phụ với giá trị bất kì mà c quyết định p
>- Mệnh đề c được đánh giá bằng cả true và false
>- Mệnh đề phụ không cần phải có giá trị giống nhau khi mệnh đề chính là true hoăc là false
>- cj(ci = true) = cj(ci = false) đối với tất cả cj 
>  hoặc
>  cj(ci = true) != cj(ci = false) đối với tất cả cj
>  **Lấy các bộ test case từ ACC thỏa mãn có cj khác nhau hoặc giống nhau là được, không cần phải quan tâm giá trị của P có khác nhau hay không**

**NOTE**: GACC thỏa mãn được CC nhưng không thỏa mãn được PC

## CACC
>- Với mỗi mệnh đề ci trong P, chọn các mệnh đề phụ cj sao cho ci quyết định p
>- Mệnh đề ci được đánh giá true hoặc false trong các test case
>- Các giá trị được chọn cho các mệnh đề phụ cj phải khiến P đúng với một giá trị của mệnh đề chính ci và sai đối với giá trị khác của ci
>- P(ci = true) != P(ci = false)
>- Các mệnh đề phụ không cần phải giống nhau
**>Lấy các cặp test case từ GACC có các giá trị P khác nhau là được**

## RACC
>- Vói mối mện đề P, mới mỗi mệnh đề chính ci trong P, chọn mệnh đề phụ cj sao cho ci quyết đinh P. ci đánh giá bằng cả giá trị true và false trong các test case
>- P đánh giá true trong một test case của mệnh đề chính và false trong các trường hợp còn lại
>- Giá trị chọn jcho mênh đề phụ cj phải giống nhau khi ci được đánh giá true cũng như là lúc được đánh giá false
>**Lấy các cặp test case từ CACC mà có các giá trị cj giống hệt nhau**


# Kiểm thử luồng điều khiển
##### def(X): là khi biến được chỉnh sửa giá trị
##### use(X): là khi biển được sử dụng giá trị
##### - p_use(X): là khi biến X được sử dụng như là điều kiện
##### - c_use(X): là khi biến X được sử dụng để tính toán

## Các thuật ngữ khác
### def_clear_path(v): là một đường dẫn được định nghĩa clear với biến v nếu như không có sự tái định nghĩa biến v trong đường dẫn đó

### complete_path: là đường dẫn bắt đầu từ node khởi đầu tới node cuối của 

### du_pair(v)
>- d là node định nghĩa của v
>- u là node hoặc cạnh sử dụng v
>	- Khi nó là p_use của v, u là một cạnh của cậu lệnh rẽ nhánh
>- có một def_clear_path của v từ d tới u


## Các tiêu chí kiểm thử bao phủ luồng dữ liệu
### All-defs coverage: **bao phủ tất cả các điểm định nghĩa trên đồ thị**
>Đối với mọi điểm def(x) trên đồ thị, tồn tài một đường def_clear_path đi qua đỉnh đấy

### All-uses coverage: **bao phủ các điểm sử dụng dữ liệu trên đồ thị**
>Đối với mọi điểm use(X) trên đồ thị, phải bao phủ được tất cả các cặp DU_pair mà nó có

### All-du-paths coverage: **bao phủ tất cả các đường dẫn DU trên đồ thị**
>


##### DU-Path
- Một đường dẫn <n1, n2, ..., nj, nk/> là một du-path gắn với biến v, nếu như biến v được định nghãi ở node n1
	- Có c-use(v) ở node nk và <n1, n2, ...., nj, nk/> là một def-clear-path
	- Có p-use(v) tại cạnh <nj, nk.> và <n1, n2, ..., nj> là một def-clear-path 









