# COW

## COW(Copy-on-Write)란?

컴퓨터 프로그래밍에서 복사 동작을 할 때,

실제 원본이나 복사본이 수정되기 전까지는 복사를 하지 않고 원본 리소스를 공유

원본이나 복사본에서 수정이 일어날 경우, 그때 복사하는 작업을 함

Swift에선 Collection Type을 복사해서 사용할 때 일어남

실제 복사를 늦추어 힙 할당을 줄이는 최적화 방법!

```swift
var array1: [Int] = [1, 2, 3, 4]
```

![image.png](COW/image.png)

```swift
var array2: [Int] = arrary1
```

array1의 값을 array2에 대입했을 때, array는 구조체 형식이기 때문에

array1에서 array2로 값 복사가 일어났다는 것!

**원래대로라면**

![image.png](COW/image%201.png)

array2가 바로 새로운 메모리를 할당해서 array1의 값을 복사해 들고 있어야 정상이지만

### COW를 쓰면 바로 복사를 하지 않음

![image.png](COW/image%202.png)

COW를 사용하면 이것처럼 array2가 array1을 참조하고 있는 형태가 됨

### 그.러.다

원본(array1)이나 복사본(array2) 둘 중 하나를 수정한 그 시점에 `array1[0] = 1`

찐 복사가 일어나서 array2의 값이 메모리에 할당됨

![image.png](COW/image%203.png)

※ Swift로 돌려보면 실제 수정이 일어나야 주소값이 바뀌고

원본이든 복사본이든 수정이 먼저 일어난 친구의 주소값이 바뀜 ※

## 장점 / 사용 이유

실제 수정이 이뤄질 때 복사를 하고, 그 전엔 참조를 통해 불필요한 복사를 줄이기 위해

COW를 사용가면 값 타입의 장점(의도하지 않은 상태 공유가 발생하지 않음)을 유지하면서

value semantic 때문에 매번 복사가 일어나며 생기는 불필요한 힙 할당을 줄일 수 있음