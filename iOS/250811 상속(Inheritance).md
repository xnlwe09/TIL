# 상속(Inheritance)

생성일: 2025년 8월 11일 오후 2:34

## 상속(Inheritance)이란?

**클래스가 다른 클래스로부터 메서드, 프로퍼티 등을 물려받는 것**

단일 상속만 해야함

## 서브 클래싱(subclassing)

<aside>

기본 클래스를 기반으로 새로운 클래스를 만드는 작업

서브 클래스 이름 옆에 : 를 쓰고 가장 먼저 상속 받고자 하는 슈퍼 클래스의 이름을 작성

</aside>

## 클래스(Class) 종류

<aside>

### 📍기본 클래스(Bass Class)

아무 클래스도 상속 받지 않는 클래스

```swift
class Human {
	var name: String?
	var age: Int?
}
```

```swift
class Human: Hashable {
	var name: String?
	var age: Int?
}

근데 이것도 기본 클래스임 !!
Hashable은 클래스가 아니라 프로토콜이기 때문에
// 시간이 되면 프로토콜도 공부를 해봅시당

결국 기본 클래스(Bass Class)는 : 뒤에 **클래스**가 붙지 않아야 기본 클래스가 되는 것임
```

</aside>

<aside>

### 📍슈퍼 클래스(Super Class) / 부모 클래스

어떤 클래스에게 자신의 특성을 물려줄 클래스

```swift
class Worker {
	var name: String?
	var position: String?
}
```

</aside>

<aside>

### 📍서브 클래스(Sub Class) / 자식 클래스

특성을 물려받는 클래스

```swift
class Worker {
    var name: String?
    var position: String?
}

// 서브 클래스(Sub Class) / 자식 클래스
class Developer: Worker {
    var language: String = "Swift"
}

class Designer: Worker {
    var tool: String = "Figma"
}

let dev = Developer()
//Developer 클래스 = “개발자”라는 직업에 대한 청사진
//Developer() = 진짜 사람 한 명 채용
//dev = “이 사람 이름표”
dev.name = "주희"
dev.position = "개발자"

let des = Designer()
des.name = "희주"
des.position = "디자이너"

// 클래스로 부모 클래스 프로퍼티에 접근할 수 없고
// 자식 클래스의 인스턴스를 생성해서 부모 클래스 프로퍼티에 접근 해야댐
```

```swift
## 프로퍼티 뿐만 아니라 메서드, 서브스크립트, 생성자도 가능데스

class Worker {
    var name: String?
    var position: String?
    
    func introduce() {
        print("My name is \(name ?? "Unknown")") // 값이 nil이면 Unknown 출력
    }
}

class Developer: Worker {
    var language: String = "Swift"
}

class Designer: Worker {
    var tool: String = "Figma"
}

let dev = Developer()
dev.name = "주희"
dev.position = "개발자"

let des = Designer()
des.name = "희주"
des.position = "디자이너"

// 부모 클래스(Worker)의 introduce() 메서드도 사용 가능
dev.introduce() // My name is 주희
des.introduce() // My name is 희주

```

</aside>

## 상속 금지 (final)

<aside>

상속이나 재정의를 금지

아무 클래스도 final이 붙은 클래스를 상속받을 수 없음

```swift
final class Worker {
	var name: String?
	var position: String?
}
```

</aside>