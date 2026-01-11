# 옵셔널(optional)

생성일: 2025년 8월 6일 오후 2:35

## 옵셔널(optional)이란?

**어떤 변수에 값이 있을 수도, 없을 수도(nil일 수도) 있는 임의의 상태를 정의내리는 것**

## 옵셔널(optional)의 사용

<aside>

Swift에서는 C언어와는 다르게 직접 Null 값을 넣을 수 없고 해당 타입의 어떠한 값이 할당이 되어야함

옵셔널은 값이 없을 수도 있다는 상황을 표현하기 위해 사용

```swift
var name: String = "주희" // 값이 있어야 함
var nickname: String? // 값이 없을 수도 있음
// = nil을 작성하지 않아도 자동으로 nil이 할당되는 것과 같은 상태가 됨
```

</aside>

## 옵셔널 언래핑(optional unwrapping)이란?

옵셔널 타입(Int?, String?)은 값이 있을 수도, 없을 수도 있기 때문에

그냥은 값을 꺼내 쓸 수 없고, 언래핑(unwrap) 해서 내부 값을 꺼내야 함

## 옵셔널 언래핑(optional unwrapping)의 종류

<aside>

### 📍강제 추출(forced unwrapping)

! 를 사용하여 강제로 언래핑하는 방법 (박스 찢기)

```swift
var name: String? = "iOS"
print(name!)       // "iOS"

// 옵셔널 변수 뒤에 ! 를 붙여서 값에 직접 접근
```

</aside>

<aside>

### 📍암시적 추출 옵셔널(Implicitly Unwrapped Optional)

처음엔 nil일 수 있지만 한 번 값이 설정된 후엔 무조건 값이 있다고 간주하는 옵셔널

! 를 붙여서 선언, 여전히 옵셔널이지만 마치 일반 변수처럼 사용할 수 있음

But 값이 없는데 접근하면 앱이 죽기 때문에 값이 있다고 확신할 때만 사용

```swift
var name: String! = "iOS"
print(name)        // "iOS"

//변수 선언 시부터 ! 를 써서 항상 자동으로 언래핑 되게 만듦
```

</aside>

<aside>

### 📍옵셔널 바인딩(optional binding)

안전하게 옵셔널을 벗겨내는 방법 (칼로 박스테이프 예쁘게 긋기)

```swift
## if let
옵셔널 값을 받아낼 상수를 만들어 nill이 아닌 경우 {}의 코드를 실행
여기서 만든 상수는 해당 if문 안에서만 사용 가능

var someNumber: Int?
someNumber = 17

if let age = someNumber {
	print(age) // 17 출력
} else {
	printf("나이 없음") //someNumber의 값이 nil일 경우
}
```

```swift
## guard let
옵셔널 값을 받아낼 상수를 만들어 nil이 아닌 경우 그 다음 코드를 실행
nil이 아닌 경우엔 else를 작성하는데, 제어 전달문(Control Transfer Statement)을 사용해야함

var someNumber: Int?
someNumber = 17

func inputAge() {
    guard let age = someNumber else {
        return print("나이 없음") //nil일 때
    }
    print(age) //nil이 아닐 때
}

inputAge() // 함수 호출 -> 17 출력
//someNumber가 nil이라면 "입력한 나이가 없습니다."을 출력
```

</aside>

<aside>

### 📍옵셔널 체이닝(optional chaining)

연쇄적으로 프로퍼티, 메소드, 서브스크립트의 값이 nil인지 확인하는 과정

옵셔널 변수 뒤에 ? 를 붙임

→ 옵셔널 값이 nil이면 전체 결과가 nil이 되고 (nil 반환),

nil이 아니면 그 다음 동작을 계속 이어서(chain) 실행함

```swift
person.contacts?.residence?.address

//person 인스턴스의 프로퍼티들이 nil인지 확인하고
//둘 다 값이 존재하면 address를 도출
```

</aside>

> **?가 타입 뒤에 붙으면 → 옵셔널 타입(Optional Type)**
ex) String? 는 String 값이 있을 수도 있고, 없을 수도 있다는 뜻
> 

> **?가 값(변수) 뒤에 붙으면 → 옵셔널 체이닝(Optional Chaining)**
> 

```swift
var name: String?         // 옵셔널 타입 선언
name = "주희"

let count = name?.count   // 옵셔널 체이닝 : name이 nil이 아니면 count 반환, nil이면 nil 반환
```
