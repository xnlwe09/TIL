# 프로토콜(Protocol)

생성일: 2025년 8월 20일 오후 10:26

## 프로토콜(Protocol)이란?

**어떤 기능에 적합한 특정 메서드, 프로퍼티 및 기타 요구 사항의 청사진(Bluprint)**

**프로토콜은 클래스, 구조체, 열거형에 의해 채택되며, 프로토콜에 정의된 요구사항의 실제 구현을 제공**

⇒ 프로퍼티/메서드에 대한 껍데기만 제공하되, 실제 구현은 채택한 곳에!

클래스 = 인스턴스를 만들기 위한 설계도

프로토콜 = 여러 설계도들이 따라야 하는 표준 규칙

## 프로토콜(Protocol) 정의하기

<aside>

실제 구현보다 이런 프로퍼티/메서드는 꼭 필요하다는, 해당 기능에 필요한 요구 사항을 선언해두는 것

```swift
// protocol for cookie

protocol Cookie {
	var flour: String { get set }
	var egg: String { get set }
	var milk: String { get set }
	
	func bake()
}
```

</aside>

---

## 프로토콜(Protocol)에서의 프로퍼티 선언

<aside>

### 📍저장 프로퍼티를 구현하던, 연산 프로퍼티를 구현하던 노상관

```swift
class ChocolateChip: Cookie {
	var flour: String = "Step1"
	var chocolatechip: String = "Step4" // 저장 프로퍼티
}

class CranBerry: Cookie {
	var flour: String = "Step1"
	var cranberry: String {
		return "Step4" // 연산 프로퍼티
	}
}
```

</aside>

## 프로토콜 내 프로퍼티는 var로 선언

연산 프로퍼티는 let은 사용할 수 없고  항상 var로 선언해야 하며

저장 프로퍼티는 { get set }에 따라서 let / var의 속성이 달라질 수 있음

<aside>

### 📍{ get }

저장 프로퍼티의 경우 let / var 선언 모두 가능

연산 프로퍼티의 경우 getter(get-only) / getter & setter 선언 모두 가능

**저장 프로퍼티**

```swift
protocol Cookie {
	var flour: String { get }
}

class ChocolateChip: Cookie {
	let flour: String = "Step1"
}

class CranBerry: Cookie {
	var flour: String = "Step1"
}
```

**연산 프로퍼티**

```swift
protocol Cookie {
	var flour: String { get }
}

class ChocolateChip: Cookie {
	var flour: String {
		get {
			return "Step1"
			}
		}
	}
	
class CranBerry {
   private var _flour: String = "Step1"
   var flour: String {
       get { return _flour }
       set { _flour = newValue }
    }
}
```

get은 초기값을 반환만 할 수 있고 set을 쓰면 그 초기값 말고 다른 값으로 변경해서 반환할 수 있음 !!

</aside>

<aside>

### 📍{ get set }

저장 프로퍼티의 경우 var로만 선언 가능

연산 프로퍼티의 경우  getter & setter로 선언해야 함

**저장 프로퍼티**

```swift
protocol Cookie {
	var flour: String { get set }
}

class ChocolateChip: Cookie {
	var flour: String = "Step1"
}

class CranBerry: Cookie {
	var flour: String = "Step1"
}
```

**연산 프로퍼티**

```swift
protocol Cookie {
	var flour: String { get }
}

class ChocolateChip {
   private var _flour: String = "Step1"
   var flour: String {
       get { return _flour }
       set { _flour = newValue }
    }
}
	
class CranBerry {
   private var _flour: String = "Step1"
   var flour: String {
       get { return _flour }
       set { _flour = newValue }
    }
}
```

</aside>

---

## 프로토콜(Protocol) 채택하기

<aside>

프로토콜을 선언함으로써, 어떤 기능을 구현하기 위한 일종의 약속을 만들어둔 것

그 프로토콜을 클래스, 구조체, 열거형이 채택하여 사용할 수 있게끔 만들 수 있음

**⇒ 프로퍼티/메서드에 대한 껍데기만 제공하되, 실제 구현은 채택한 곳에!**

```swift
protocol Cookie {
	var flour: String { get set }
	var egg: String { get set }
	var milk: String { get set }
	
	func bake()
}

class ChocolateChip: 상속받을 클래스, Cookie { // 프로토콜 채택
	var flour: String = "Step1"
	var egg: String = "Step2"
	var milk: String = "Step3"
	var chocolatechip: String = "Step4"
	
	func bake() {
		print("초코칩 쿠키를 굽자")
	}
}

let myCookie = ChocolateChip()
// myCookie가 ChocolateChip 클래스의 인스턴스가 되도록 하고
// 그래서 ChocolateChip의 인스턴스가 된 myCookie로 프로퍼티에 접근
print(myCookie.flour) // Step1
print(myCookie.chocolatechip) // Step4
myCookie.bake() // 초코칩 쿠키를 굽자
```

</aside>

## optional로 프로퍼티/메서드 선언하기

<aside>

필수적이지 않은 요소도 프로토콜(protocol)에 선언하고 싶을 때

- Swift 순수 프로토콜에서는 optional 키워드가 없음
- Objective-C 런타임에 호환되도록 해야 @objc optional을 쓸 수 있음
- 그래서 @objc protocol에서만 옵셔널 프로퍼티나 메서드를 정의할 수 있다

```swift
@objc protocol Cookie {
	var flour: String { get set }
	var egg: String { get set }
	var milk: String { get set }
	@objc optional var butter: String { get set }
	
	func bake()
}
```

```swift
@objc protocol Cookie: AnyObject {
	var flour: String { get set }
	var egg: String { get set }
	var milk: String { get set }
	@objc optional var butter: String { get set }
	
	func bake()
}

class ChocolateChip: NSObject, Cookie { // NSObject 상속
	var flour: String = "Step1"
	var egg: String = "Step2"
	var milk: String = "Step3"
	var chocolatechip: String = "Step4"
	var butter: String? = "Step5"
	
	func bake() {
		print("초코칩 쿠키를 굽자")
	}
}

// 온라인 Swift 실행기 등에서는 Objective-C 호환이 비활성화돼 있음
// @objc와 NSObject는 Mac/iOS 환경의 Objective-C 런타임이 있어야만 동작
```

</aside>

```swift
// Swift 옵셔널

protocol Cookie {
	var flour: String { get set }
	var egg: String { get set }
	var milk: String { get set }
	var butter: String? { get set } // Swift 옵셔널
	func bake()
}

class ChocolateChip: Cookie {
	var flour: String = "Step1"
	var egg: String = "Step2"
	var milk: String = "Step3"
	var chocolatechip: String = "Step4"
	var butter: String? = "Step5" // Swift 옵셔널
	
	func bake() {
		print("초코칩 쿠키를 굽자")
	}
}
```

<aside>

Swift 옵셔널(String?)

- 컴파일 시 타입이 정해져 있어야 함
- 런타임에 “이 메서드가 구현돼 있는가?”를 체크할 수 없음
- Swift 옵셔널을 프로토콜에서 정의하면, 그 속성 자체는 옵셔널 타입이 되지만, 프로토콜 요구 사항으로 선언된 메서드는 반드시 구현해야 함 = 선택적 프로퍼티/메서드 구현 안하면 에러남

@objc optional

- Objective-C 런타임이 구현 여부를 체크
- 클래스가 @objc protocol을 채택했지만 선택적 메서드를 구현 안 해도 안전하게 호출 가능
</aside>

## 프로토콜(Protocol)에서의 mutating

<aside>

mutating 복습하기

[구조체(Struct)](https://www.notion.so/Struct-255933c2941a81b69c6cfa753ef59d77?pvs=21)

</aside>

<aside>

### mutating이 필요하면 프로토콜 자체에 추가

구조체의 경우 메서드 안에서 프로퍼티 값을 변경해야 할 경우 mutating이란 키워드를 func 앞에 작성

→ 프로토콜에서는 mutating도 같이 프로토콜에 선언해주면 됨

```swift
// 프로토콜 정의
protocol Cookie {
    var flour: String { get set }
    var egg: String { get set }
    var milk: String { get set }
    
    mutating func bake() // mutating 작성
}

// 구조체
struct ChocolateChip: Cookie {
    var flour: String = "Step1"
    var egg: String = "Step2"
    var milk: String = "Step3"
    var chocolatechip: String = "Step4"
    
    mutating func bake() {
        print("초코칩 쿠키를 굽자")
        // 프로퍼티 값 변경
        flour = "Step1 - 필요한 재료"
        chocolatechip = "Step4 - 초코칩을 넣어야 해"
    }
}

var myCookie = ChocolateChip()
print(myCookie.flour) // Step1
print(myCookie.chocolatechip) // Step4

myCookie.bake() // 초코칩 쿠키를 굽자

print(myCookie.flour) // Step1 - 필요한 재료
print(myCookie.chocolatechip) // Step4 - 초코칩을 넣어야 해
```

구조체는 값 타입이니까 값이 복사되는 거임

→ 메서드 안에서 자기 자신의 프로퍼티를 바꾸려면 **복사본을 수정**해야 함

→ mutating 메서드는 인스턴스가 변수(var)여야 호출 가능

</aside>