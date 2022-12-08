# Thuật ngữ và khái niệm
## Quản lý state
Xem qua đoạn code dưới đây, thực hiện track một số và tăng số đó lên khi mà button được click

```jsx
function Counter() {  
// Biến counter là biến lưu trạng thái số lần được click
const [counter, setCounter] = useState(0)  
  
// Hành động increment thực hiện tăng giá trị của biến counter lên một đơn vị
const increment = () => {  
setCounter(prevCounter => prevCounter + 1)  
}  
  
// UI được hiển thị
return (  
<div>  
Value: {counter} <button onClick={increment}>Increment</button>  
</div>  
)
```

Trên đây là một ví dụ về "one-way data flow"
- State biểu diễn điều kiện của app tại một thời điểm nhất định
- UI hiển thị dựa trên state
- Khi một cái gì đó xảy ra (ví dụ như người dùng click), trạng thái được cập nhật dựa trên những gì đã xảy ra
- UI tự render lại dựa trên trạng thái mới
![[Pasted image 20221203152011.png]]

Tuy nhiên, sự đơn giản này bị phá vỡ khi mà chúng ta có nhiều component và chúng cần chia sẻ và sử dụng trạng thái của nhau. Cụ thể, nếu như những component được sử dụng ở những phần khác nhau của app. Thỉnh thoảng chúng ta có thể phải giải quyết bằng "lifting state up" (truyền ngược data lên cho cha mẹ trong cây componet), nhưng đó luôn luôn không phải là một cách.

Một cách nữa để có thể giải quyết đó chính là triển khai những trạng thái chúng từ những component này ra, và để nó vào trung tâm, bên ngoài component tree. Với thứ này, component tree trở nên rất lớn, và bất kì component nào cần truy cập vào tstate hoặc kích hoạt một action nào đó thì nó sẽ không cần biết chúng ở đâu trên cây nữa

Bắng cách định nghĩa và chia nỏ khải niệm bên trong state management và triển khai các quy tăng để có thể duy trì độc lập giữa UI và state, chúng là làm cho code trở nhên có cáu trúc và để bảo trì

Đây chính là ý tưởng cơ bản đằng sau Redux: một vị trí dơn lể chứa các global state bên trong app, và các mẫu để có thể bám theo và cập nhất trạng khái để làm cho code trể nên có thể dự đoán được


## Immutability - Sự bất biến
Mutable có nghĩa là có khả năng thay đổi. Nếu một thứ nào đó là "immutable", chúng không bao giờ có thể bị thay đổi
Object trong JS và mảng mặc định là mutable. Nêu tạo một Object, ta có thể thay đổi định nghĩa các trường của nó. Nếu ta tạo một cái mảng, ta cũng có thể thay đổi nội cdung của nó
```JS
const obj = { a: 1, b: 2 }  
// cùng là một đối tượng nhưng nội dung đã bị thay đổi
obj.b = 3  
  
const arr = ['a', 'b']  
// Cùng một cách, chúng ta có thể thay đổi nội dụng của mảng này  
arr.push('c')  
arr[1] = 'd'
```

Trên đây được gọi là "mutating" đối tượng / mảng.  Nó chính là thể hiện của đối tượng và mảng trong bộ nhớ, nhưng hiện tại nội dung bên trong đối tượng đã bị thay đổi

**Để có thể update những giá trị immutably (bất biến), code của bạn sẽ phải tạo ra các bản copy từ những đối tượng / mảng, và sau đó thay đổi các bản copy đó**

Chúng ta có thể làm điều này bằng tay sử dụng JS Array / Object spread operator

# Các khái niệm
Các khái niệm quan trọng trong Redux mà bạn cần biết trước khi bắt đầu

## Actions
Một hành động là một đối tượng JS có trường "type". Bạn có thể nghĩ là một hành động như là một event miểu tả một cái gì đó đã xảy ra với app của bạn

Trường type nên là string và nên cho nó một cái tên mang tính miêu tả, như là "todos/todoAdded". Chúng tôi thường viết type string kiểu như "domain/eventName", nơi phần đầu tiên của tính năng / mà hành động này thuộc về, và phần thứ 2 là phần cụ thể thứ gì đã xảy ra

Một đối tượng hành động có thể có những trường khác với các thông tin thêm vào về cái gì đã xảy ra. Như là một thủ tục, chúng tôi cho tất cả các thông tin vào bên trong trường payload

Một đối tượng hành động trông như thế này
```JS
const addTodoAction = {
	type : 'todos/todoAdded',
	payload : 'Buy Milk'
}
```

## Action Creators
Một Action Creator là một hàm mà tạo và trả về một action object. Sử dụng cách này sẽ khiến chúng ta khôn gcaanf phải viết lại Action Object bawngff tay mỗi lần
```JS
const addTodo = text => {
	return {
		type : 'todos/todoAdded',
		payload : text
	}
}
```
## Reducers
Một reduceer là một function, chúng nhận state hiện tại và một đối tượng hành động (action object) sau đó quyết định cách update trạng thái hiện tại như nào. Chúng luôn trả về một trạng thaismoiws. Bạn có thể nghĩ về reducer như là một event listener thứ mà sẽ handle các sự kiện dựa trên những hành động mà chúng nhận được

Các reducre phải luôn luôn theo các rule sau:
	- Chúng chỉ nên tính toán trạng thái mới dựa trên trạng thái và hành động
	- Chúng không được phép chỉnh sửa trạng thái đang tồn tại. Thay vào đó, chúng thực hiện immutable update, bằng các copy trạng thái đang tồn tại và thực hiện thay đổi trên trạng thái vừa được copy

Chúng ta sẽ nói nhiều hơn về các quy tắc của reducer sau bao gồm các sự quan trọng của chúng và làm sao để có thể sử dụng chúng đúng các

Logic bên trong những reducer function thường giống như là "tập các bước"
- Kiểm tra nếu như reducer quan tâm tới hành động
	- Nếu có, thực hiện copy state, cập nhật state copy và trả lại 
- Nếu không, trả lại trạng thái không thay đổi của hiện tại

Đây là một ví dụ về một reducer, chỉ ra các bước mà mỗi reducer phải làm theo:
```JS
const initialState = {value : 0};
function coutnerReducer(state = initialState, action) {
	// Kiểm tra xem nếu như reducer quan tâm tới hành động action
	if (action.type === 'counter/increment') {
		// Thực hiện copy state
		return {
			...state,
			// thực hiện cập nhất bản vừa mới copy với giá trị mới
			value : state.value + 1
		}
	}
}
```

Reduce có thể sử dụng bất kì logic nào bên trong để thực hiện ra quyết định trạng thái mới nên được : if/else, switch, vòng lặp ...

## Store
Trạng thía hiện tại của một Redux up được lưu bên trong một Object gọi là store
Store được tạo bằng cách đẩy vào nó một reducer, và có một phương thức để gọi là getState để lấy được state hiện tại
```JSX
import { configureStore } from '@reduxjs/toolkit'

const store = configureStore({ reducer : counterReducer })

console.log(store.getState())
```

## Dispatch
Redux store có một phương thức gọi là dispatch. Các duy nhất để thưc hiện cập nhật trạng thái đó chính là gọi ==store.dispatch()== và đẩy vào bên trong đó một ==action object==. Store có thể chạy bất cứ hàm nào của reducer và lưu chúng vào một state mới, và sau đó chúng ta có thể gọi getState() để có thể lây được giá trị đã update
```JS
store.dispatch({type : 'counter/increment'});
console.log(store.getState())
```
Bạn có thể nghĩa về dispatching actiuon như là "trigger một hành động" bên trong app.  Một thử gì đó xảy ra và chúng ta muốn store có thể biết về nó. Reducers hành động như là một event listener, và khi chugns nghe thầy một hành động, chúng biết được và chúng update trạng thái 

Chúng ta thường gọi action creator để có thẻ dispaltch hahf động đúng
```JS
const increment = () => {
	return {
		type : 'counter/increment'
	}
}
store.dispatch(increment())
console.log(store.getState())
```

## Selectors
Selectors là một hàm mà chúng biết cách để trích xuất những mẩu thông tin nhỏ nhất định từ một store chứa trạng thái. Như một cái app phát triển trở nên lớn hơn, thứ này có thể giúp tránh được việc lặp logic ở các phần khác nhau của app khi cần đọc data cùng một dạng data
```JS
const selectCountervalue = state => state.value

const currentValue = selectCounterValue(store.getState())
```

# Redux Application Data Flow

Trước đó chugns ta đã nói về "one-wayj data flow" - miêu tả chuỗi các bước để thực hiện cập nhật trong app
- State miêu tả tình trạng hiện của app tại một thời điểm
- UI hiển thị dựa trên state
- Khi một hứ gì đó thayd dổi, trạng thái được cập nhật dựa trên cái gì đang diễn ra
- UI thực hiện rerender dựa trên trạng thái mới
Với Redux, chúng ta có thể chia nỏ các bước vào các thông tin chi tiết sau
- Initial setup:
	- Một Redux store được tạo sử dụng hàm reducer gốc
	- Store gọi hàm reducer gốc một lần và thực hiện lưu giá trị trả về như là giá trị state khởi đầu
	- Khi thành phần UI lần đầu được render, UI Component truy cập vào state hiện tại của Redux store, và sử dụng data đó để quyết định cái gì được hiển thị. Chúng cũng thực hiện đăng kí để khi sotre update trong tương lai, chugns có thể biết nếu như trạng thái thay đổi
- Update
	- Một thứ gì đó xảy ra bên trong app (ví dụ như click vào một button)
	- App dispatche ra một hành động tới Redux store, kiểu như ```JS dispatch({type : 'counter/increment'})```
	- Store chạy hàm reducer lại một lần nữa với trạng thái trước đó và hành độn hiện tại, lưu và trả về một trạng thái mới
	- Store lại thông báo cho tất cả các htnahf phàn UI mà đã đăng kí lắng nghe khi store cập nhật
	- Mỗi thành phần Ui cần dât từ store thực hiện check lại để xem thử xem trạn thái mà chúng cần có được thay đổi hay không
	- Mỗi thành phần sẽ thấy dât được thay đôi và thực hiện forece re-render với dât mới, chugsn có thể update những gì mà chúng hiển thị trên màn hình]
Dưới đây là cách mà dataflow hoạt động![[reduxdataflowdiagram-49fa8c3968371d9ef6f2a1486bd40a26.gif]]
