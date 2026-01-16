# Initializer(초기화)

생성일: 2025년 8월 20일 오후 10:26

## Initializer(초기화)란?

**구조체 / 열거형 / 클래스의 인스턴스를 생성하는 것**

초기화의 역할 : 모든 프로퍼티를 기본값으로 초기화 하는 것

→ 인스턴스 내 기본값이 존재하지 않는 프로퍼티가 있을 경우 초기화에 실패하고 인스턴스는 생성되지 않음

## 구조체(Struct) 초기화하기

<aside>

### 📍선언 + 기본값

프로퍼티를 선언함과 동시에 기본값을 넣어서 초기화할 수 있음

```swift
struct Human {
	let name: String = "주희"
	var age: Int = 17
}
```

</aside>

<aside>

### 📍프로퍼티 타입을 옵셔널(optional) 타입으로 설정

초기화를 할 때 옵셔널 타입인 프로퍼티들은 자동으로 nil로 초기화 됨

```swift
struct Human {
	let name: String?
	var ag: Int?
}
```

</aside>

<aside>

### 📍init 함수에서 값 설정

생성자(init) 안에서 해당 프로퍼티들을 초기화

```swift
struct Human {
	let name: String
	var age: Int
	
	init(){
		self.name = "주희"
		self.age = 17
	}
}
```

</aside>

<aside>

### 📍근데 사실 구조체는 초기화 안해도 됨 → Memberwise Initializer가 있으니까!

Memberwise Initializer는 구조체가 자동으로 제공하는 생성자

프로퍼티의 초기화를 따로 지정하지 않을 경우, 초기화되지 않은 프로퍼티를

초기화할 수 있는 init 함수를 자동으로 제공

```swift
struct Human {
	let name: String?
	var ag: Int?
}
```

### Memberwise Initializer로 제공되는 생성자의 파라미터

프로퍼티가 선언된 순서와 갯수에 맞추어 생성되고 파라미터의 이름은 프로퍼티의 이름으로 설정됨

```swift
struct Human {
	let name: String
	var name: Int
}

Human.init(name:"주희", age: 28)
// 이거 순서 안지키면 오류남
```

### **프로퍼티가 let으로 선언 되어 있을 때**

이미 초기화가 되어있는 상태면(초기값을 가지고 있을 때) 생성자 목록에서 제외

```swift
struct Human {
	let name: String = "주희"
	let age: Int
}

Human.init(age:28)
// 초기값이 있는 name은 제외임
```

### 생성자를 직접 생성하면 Memberwise Initializer는 더이상 미제공

구조체는 생성자를 따로 구현하지 않은 상황에 한해서 Memberwise 라는 생성자를 자동으로 제공함

(그냥 Memberwise는 기본 생성자임) 근데 구조체에서 생성자를 직접 구현해버리면

Memberwise lnitializer를 더이상 제공하지 않는데 extension으로 생성자를 추가하면

Memberwise Initializer를 보존하면서 생성자를 추가할 수 이씀

- 이상 extension의 한 부분 -

</aside>

## 클래스(Class) 초기화하기

<aside>

### 📍선언 + 기본값

프로퍼티를 선언함과 동시에 기본값을 넣어서 초기화할 수 있음

```swift
class Human {
	let name: String = "주희"
	var age: Int = 17
}
```

</aside>

<aside>

### 📍프로퍼티 타입을 옵셔널(optional) 타입의 변수로 설정

초기화를 할 때 옵셔널 타입 변수 프로퍼티들은 자동으로 nil로 초기화 됨

```swift
struct Human {
	var name: String?
	var ag: Int?
}

// let 상수 안돼염
```

</aside>

<aside>

### 📍init 함수에서 값 설정

하나의 프로퍼티라도 기본 값을 가지고 있지 않거나 옵셔널 타입의 변수가 아니라면

init 함수(생성자)를 통해 초기화를 해줘야 함 (생성자 안에서 해당 프로퍼티들을 초기화 할 수도 있음)

모든 프로퍼티가 기본 값을 가지거나 옵셔널 타입 변수이거나 초기값을 갖는다면

생성자를 따로 선언해줄 필요 없씀

```swift
class Human {
    var name: String?
    let nickName: String = "희주"
    let age: Int
    
    init(name: String) {
        self.age = 17
    }
}
```

</aside>

## 클래스(Class)의 Initializer

<aside>

### 📍지정 생성자(Designated Initializer)

클래스의 모든 프로퍼티를 초기화 하는 생성자 = 그냥 우리가 쓰던 init임

**1️⃣ 해당 생성자 메서드가 종료되기 전까지 생성자 안에 모든 프로퍼티는 초기값을 가지고 있어야함**

**2️⃣ 반드시 super 클래스의 생성자를 호출해야함**

상속 받은 서브 클래스에서 Designated Initializer를 작성할 경우

반드시 슈퍼 클래스의 Initializer 호출

</aside>

<aside>

### 📍편의 생성자(Convenience Initializer)

</aside>