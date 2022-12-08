# App Counter
Dự án ví dụ này, chúng ta sẽ nhìn vào một ứng dụng đêm counter cho phép chúng ta bên / bớt từ một số khi chúng ta click. Nó có thể không đủ thích thú nhưng nó cho tat tháy được tất cả các thành phần quan trọng của một React+Redux app

Dự án này được tạo bằng cách sử dụng template chính thức của Redux dành cho [Create-React-App](https://github.com/reduxjs/cra-template-redux) Ngoài ra, nó đã config sẵn cấu trúc tiêu chuản của một Redux app, sử dụng Redux Toolkit để tạo Redux store và logic, và React-Redux ddeer kết nốt cùng với Redux Store và React components

# Khởi tạo Redux Store
Trong file ```app/store.js```, nhìn giống như sau
```JS
import { configureStore } from '@reduxjs/toolkit'
import counterReducer from '../features/counter/counterSlice'

export default configureStore({
	reducer : {
		counter : counterReducer
	}
})
```
Redux store được tạo bằng cách sử dụng hàm ```configureStore``` từ Redux Toolkit. ```configureStore``` yêu cầu chúng ta pass mà một tham số reducer

Ứng dụng của chúng ta có thẻ được tạo nên bởi nhiều các tính năng khác nhau, và mỗi trong số chúng có thể có riêng một reducer. Khi chúng ta gọi configureStore, cúng ta có thể pass tất cả các reducer khác nhau vào trong một object. Khóa bên trong object sẽ được định nghĩa trong giá trị state cuối cùng

Chúng tôi có một file tên là ```features/counter/counterSlice.js``` mà export ra một hàm reducer dành cho logic đếm. Chúng ta có thể import ```counterReducer``` vào đây, và bao gồm nó khi chúng ta tạo store

Khi chúng ta pass một đối tượng như ```{counter : counterReducer}```, điều này nói rằng chúng ta muốn có một phần ```state.counter``` của đối tượng Redux State, và chúng ta muốn hàm counterReducer có thể được ??? và cách để cập nhật state.counter khi có một hành động được đưa ra

Redux cho phép store cài đặt để có thể được custom theo nhiều loại plugin ("middleware" và "enhancer"). configureStore tự động add nhiều middleware vào bên trong store, được cài mặc định để cung cấp trải nghiệm phát triển tốt cho developer, và bên cạnh đó cài đặt store để Redux DevTools Extension có thể quan sát được nội dung của nó

## Redux Slices
Một "slice" là một bộ sưu tập về reducer logic và hành động dành cho một tính năng riêng lẻ trong app của bạn, bình thường được định nghĩa cùng nhay trong một file. Cái tên tới từ chia state object thành nhiều các state nhỏ

Ví dụ sau, trong một app blog, store của chúng ta có thể cài đặt như dưới đây
```JS
import { configureStore } from '@reduxjs/toolkit'
import usersReducer from '../features/users/usersSlice'
import postsReducer from '../features/posts/postsSlice'
import commentsReducer from '../features/comments/commentsSlice'

export defaut configureStore({
	reducer : {
		users : usersReducer,
		posts : postsReducer,
		comments : commentsReducer
	}
})
```
Ở ví dụ trên, state.users, state.posts, và state.comments được chia thành nhiều "slice" riêng biết của Redux state. usersReducer phản hồi các update của state.users clice, chúng như là một hàm "slice reducer"

## Tạo Slice Reducer và Action
Chúng ta biết rằng hàm counterReducer tới từ ```features/counter/counterSlice.js```, chúng ta hãy xem có cái gì bên trong file này, từng chút từng chút một
```JS
import { createSlice } from '@reduxjs/toolkit'

export const counterSlice = createSlice({
	name : 'counter',
	initialState : {
		value : 0
	}
	reducers : {
		increment : state => {
			// Redux Toolkit cho phép chugns ta viết "mutating" logic ở các re
			// ducer. Nó không thực sự là thay đổi state bơi vì nó sử dụng 
			// immber library, có thể xác định được những sự thay đổi tới một
			// state và sản xuất ra một immutable state miows cứng dựa trên 
			// những thay đổi
			state.value += 1;
		},
		decrement : state => {
			state.value -= 1;
		},
		incrementByAmount : (state, action) => {
			state.value += action.payload
		}
	}
})

export const { increment, decrement, incrementByAmount } = counterSlice.actions
export default counterSlice.reducer
```

Trước đó, chúng ta thấy rằng click các nút khác nhau trong UI thì vứt ra 3 loại Redux action
- {type : 'counter/increment'}
- {type : 'counter/decrement'}
- {type : 'counter/incrementByAmount'}

Chúng ta biết răng các hành động là những đối tượng với trường type, trường type luôn luôn là string, và chúng ta thường có hàm "action creator" để khởi tạo và trả về các action object. Vậy đâu là nới mà những action object, type, và action create được định nghĩa

Chúng ta có thể viết tất cả những thứ này bằng tay, mỗi lần, nhưng việc đó thật buồn chán. Bên cạnh đó, thứ thực sự quan trong trong redux chính là hàm reducer và các logic thực hình tính toán cho new state

Redux Toolkit có một hàm gọi là createSlice, nớ tham gia vào mọi công việc sinh ra action type, action creator và các action object. Tất cả bạn cần làm là định nghĩa tên cho  slice, viết một đối tượng có một vài hàm reducer trong nó và nó sẽ generate tương ứng các code hành động tương ứng một cách tự động. String bên trong trường name được sử dụng như là phần đầu tiên của mỗi action type, và key name của mỗi hàm reducer được sử dụng như là thành phần thứ hai. Bởi vậy, "counter/increment" reducer sinh ra hành động {type : "counter/increment"}.

Thêm và đó,  createSlice cần chúng ta pass trạng thái khởi đầu cho các reducer, bởi vậy có một state lần đầu tiên được gọi. Trong trường họp này, chúng ta đang cung cấp một object với trường value bắt đầu bằng 0

Chúng ta có thể thay rằng có 3 hàm reducer, và tương ứng vói 3 action time được vứt ra bằng cách click vào các nút khác nhua

createSlice tự động sinh ra các actionc creator với cái tên tương tự như là các reducer function mà chúng ta đã viết. Chúng ta có thể kiểm tra bằng cách gọi từng cái và xem cái gì trả về

Nó cũng tự sinh ra một reducer function mà có thể phản hồi lại thất cả các action type

## Các luật dành cho reducer

## Viết các logic bất đồng bộ với Thunks
Tất cả các login trong app của chúng ta thường là đồng bộ. Actions được bắn ra, store chạy các reducer và tính toán ra trạng thái mới, và hàm dispatch hoàn thành. Nhưng, JS có nhiều các để viết code, đó là bất đồng bộ (asynchronous), và app của chúng ta thường có các logic bất đồng bộ dành cho việc fetch dât từ API. Chúng ta cầm một chỗ nào đó để đem đống logic bất đồng bộ này vào bên tron Redux app

A **thunk** là một loại Redux function đặc biết mà có thể chứa bên trong nó logic bất đồng bộ. **Thunks** được viết bằng cách sử dụng hai hàm:
- Một hàm thunk bên trong, nhận dispatch và getState như là các tham số
- Một hàm khởi tạo bên ngoài, khởi tạo và trả về hàm **thunk**
Hàm tiếp theo mà được xuất ra từ counterSlice là một ví dụ về một **thunk action creator**
```JS
export const incrementAsync = amount => dispatch => {
	setTimeout(() => {
		dispatch(incrementByAmount(amout));
	})
} 
```

Chúng ta có thể sử dụng chúng giống như một hàm action creator thông tường
```JS
store.dispatch(incrementAsync(5));
```

Tuy nhiên, sử dụng thunks yêu cầu ==redux-thunk== middleware (một loại plugin dành cho Redux) được thêm vào Redux store khi mà nó được khởi tạo. May mắn thay, Redux Toolkit ==configureStore== đã tự động cài sẵn cho chúng ta, và chugns ta có thể tiếp tục sử dụng thunk ở đây

Khi bạn cần một AJAX gọi để kéo data từ server, bạn có thể để chúng gọi trong một **thunk**. Dưới dây là một ví dụ viết một cách dài dòng, bạn có thể xem cách nó được định nghĩa

```JS
// Đây là thunk creator, được viết bên ngoài
const fetchUserById = userId => {
	// Đây là thunk bên trong
	return async (dispathc, getState) => {
		try {
			const user = await userAPI.fetchById(userId)
			dispatch(userLoaded(user))
		} catch (err) {
		}
	}
} 
```

#### Giải thích cụ thể về : Thunk và Logic bất đồng bộ
Chúng ta biết răng chúng ta không được phét để bất kì logic bất đồng bộ nào vào trong reducer. Nhưng, đoạn logic đó cần được live ở nơi nào đó.

Nếu chúng ta truy cập trực tiếp vào Redux store, chúng ta có thể viết code bất động bộ và sau đó gọi store.dispatch() khi chúng ta xong
```JS
const store = configureSotre({reducer : counterReducer})
setTimeout(() => {
	store.dispatch(increment())
}, 250)
```

Nhưng, trong một app Redux thực sự, chugns ta không được phép import store vào các file khác, cụ thể hơn là các React component. Bởi vì chúng làm co code khó để test và sử dụng lại hơn

Thêm vào đó, chúng ta thường viết các logic bất động bộ mà chúng ta biết sẽ được dùng với một vài store, nhưng chúng ta không biết nó ở store nào

Redux store có thể được mở rộng bởi middleware, một loại plugin cúng cấp thêm các tính năng bên ngoài. Lý do thường lấy để sử dụng middleware là để chúng ta viết code có thể có logic bất đồng bộ bên trong, nhưng vẫn nói chuyện với store ở cùng một thời điểm. Chúng có thể thay đổi store bởi vậy chúng ta có thể gọi dispatch() và pass các gái trị không phải là một plain object, giống như fucntion và Promises

Redux Thunk middleware thay đổi store và cho phép bạn thêm các hàm vào dispatch. Sự thạt là, nó đủ nắng để chúng ta có thể paste nó vào đây
```JS
const thunkMiddleware = 
	  ({dispatch, getState}) =>
	  next =>
	  action => {
		  if (type action === 'function') {
			  return action(dispatch, getState)
		  }
		  return next(action)
	  } 
```

Nếu như action được pas vào dispatch thì thực sự là một function thay vì là một plain object. Nếu nó thực sự là một function,, nó gọi function và trả về kết quả. Còn không, nó phải là một object aciotn, 