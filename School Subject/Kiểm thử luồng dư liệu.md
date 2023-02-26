(1)------>(2)
 |               |
 |               |
 v              v
(3)----->(4)

Trong luồng CFG (control flow graph) ta quan tâm tới các node tại đó biến được định nghĩa và sử dụng
(def)-----(use) => Kiểm thử luồng dữ liieuej
## Định nghĩa
>- def(variable) => là các nốt trên CFGm tại đó biến được gán giá trị
>- use(variabl) => là các node trên CFG mà tại đó biến không thay đổi giá trị
>	- p_use
>	- c_use
>Ví dụ:
>x := x + 1
>\     \ use(x)
>\
>----- def(x)
>
>- Sử dụng trong các câu lệnh điều kiện là các node quyết định mà tại đó biến được sử dụng -> predicate_use
>p_use(x)
>Ví dụ: y  = sqrt(x) -> def(y) và use(x)
>- c_use(x) là các node != node quyết định mà tại đó biến được sử dụng 

## Các tiêu chi bao phủ
+ path : đường dẫn chương tình, là đường bắt đầu từ điểm bắt đầu đến điểm kết thức của chương trình
+ def_clear_path(x) là đường dẫn chương trình trên đó chỉ tồn tại duy nhất một node mà tại đó x được định nghĩa
+ p1 = (1 - 2 -4) là def_clear_path(x)
+ p2 = (1 - 3 - 4) là dev_clear_path(x)

- DU_pair : cặp def_use của 1 biến <d, u> là 1 cặp def-use của biến iff (nếu và chỉ nếu)
	- d là node tại đó có def(x)
	- u là node tại có có use(x)
	- tồn tại một dev_clear_path từ d tới u của x
- (def(x)) --------------(không tồn tại def(x))----------------------(use(x))
      N1                                                                                                                N2
      <N1, N2> là một cặp DU_pair
- (N1) --------------------------- (Nk)---------------(Nk-Nk+1) -> <N1, Nk-Nk+1> -> DU_pair
                                                               |
                                                               |
                                                               (Nk-Nk+2) -> <N1, Nk-Nk+2> -> DU_pair
### Ví dụ
```js
input(A, B) -> 1
if (B > 1) {
	A = A + 7; -> 2
}
if (A > 10) { -> 3
	B = A + B; -> 4
}
output(A, B) -> 5
```
(1)------B > 1 -------->(2)
 |                                        |
 |                                        |
 B<= 1                               |
 |                                        |
 V                                      |
(3)<---------------------
 |------A > 10-------->(4)
 |                                        |
 |                                        |
 A <= 10                           |
 |                                        |
 V                                      |
(5)<--------------------|

1: def(A), def(B)
2: use(A), def(A)
3: use(A)
4: use(A), use(B), def(B)
5: use(A), use(B)
|du_pair|paths|
|-|-|
|<n1,n2>|do n2 sử dụng cả use(A) và def(A)|
|<n1, n3-n4>|<n1, n3, n4>|
|<n1,n3-n5>|<n1,n3,n5|
|<n1,n4>|<n1, n3, n4>|
|<n1, n5>|<n1, n3, n5|

Đối với biến b
|du_pair|paths|
|-|-|
|<1, 1-2>|<1,2>|
|<1, 1-3>|<1,3>|
|<1,4>|<1,3,4> + <1,2,3,4>|
|<1,5>|<1,3,5> + <1,2,3,5>|
|<4,5>|<4,5>|


all_def_coverrage : bao vủ với mọi điểm định nghãi của biến
Với mọi biến, sinh các test case sao cho tồn tại ít nhất một đường dẫn def_clear_path từ (mọi dev(x)) tới ít nhất 1 use(x) 



