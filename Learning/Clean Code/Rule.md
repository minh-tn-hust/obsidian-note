# Không bao giờ được tab quá nhiều
```cpp
int calculate(int bottom, int top) {
	if (top > bottom) {
		int sum = 0;
		for (int number = bottom; number <= top; number++){
			if (number % 2 == 0) {
				sum += number;
			}
		}
		return sum;
	} else {
		return 0;
	}
}
```
Đoạn code trên có độ sau bằng 4. Có hai cách để có thể làm cho độ sâu của đoạn code nhỏ lại
## Cách 1 : Extraction
> Đối với cách này, chúng ta có thể extract các đoạn code bên trong ra thành một function riêng
```cpp
int filterNumber(int number) {
	if (number % 2 == 0) {
		return number;
	}
	return 0;
}
int calculate(int bottom, int top) {
	if (top > bottom) {
		int sum = 0;
		for (int number = bottom; number <= top; number++){
			sum += filterNumber(number);
		}
		return sum;
	} else {
		return 0;
	}
}
```
Độ sâu của chúng đã giảm đi một nửa
## Cách 2: Đưa các trường hợp return sớm lên phía trước
```cpp
int filterNumber(int number) {
	if (number % 2 == 0) {
		return number;
	}
	return 0;
}
int calculate(int bottom, int top) {
	if (top <= bottom) return 0;
	
	int sum = 0;
	for (int number = bottom; number <= top; number++){
		sum += filterNumber(number);
	}
	return sum;
}
```
Như này thì từ độ sau 4, ta xuống độ sâu 2

:))) Nhớ đừng nest code nữa, 3lv nest code 

---
# Đặt tên
## Đặt tên dễ hiểu, kèm theo đơn vị của biến bên trong tên của nó
```cpp
void execute(int delay) // wrong

void execute(int delaySeconds) // right
```

```python
class Renderer:
	def __init__(self, renderIntervalSeconds):
		self.renderIntervalSeconds = renderIntervalSeconds
```