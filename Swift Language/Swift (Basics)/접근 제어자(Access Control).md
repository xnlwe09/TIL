# 접근 제어자(Access Control)

## 접근 제어자(Access Control)란?

코드 내에서 접근 가능한 범위를 정의하여 모듈성과 코드의 캡슐화를 향상시키는 데 사용

## 접근 제어자의 종류

<aside>

### 1️⃣ open

특징 : 모듈 외부에서 접근 및 재정의 가능

사용 위치 : 클래스 및 클래스 멤버에만 사용 가능

목적 : 해당 클래스를 다른 모듈에서 확장(상속)하고, 메소드를 재정의하도록 허용

ex) 외부 모듈에서 상속과 오버라이드를 지원해야 하는 경우

```swift
open class Animal {
	open func bark() {
		printf("으르렁 으르렁")
	}
}

class Dog: Animal {
	override open func bark() {
		printf("멍멍")
	}
}
```

</aside>

<aside>

### 2️⃣ public

특징 : 모듈 외부에서 접근 가능하지만, 재정의와 상속은 불가능

사용 위치 : 클래스, 구조체, 열거형, 프로토콜 및 그 멤버

목적 : API로 제공하되, 상속 및 재정의는 허용하지 않으려는 경우

open과의 차이점 :

- open은 외부에서 상속, 재정의 가능
- public은 외부에서 접근만 가능하고 상속, 재정의 불가능

```swift
open class Animal {
	open func bark() {
		printf("으르렁 으르렁")
	}
}

// 다른 모듈에서 작성한 코드라면 재정의 불가능
class Dog: Animal {
	override open func bark() { // 에러남
		printf("멍멍")
	}
}
```

</aside>

<aside>

### 3️⃣ internal (기본값)

특징 : 모듈 내부에서만 접근 가능

사용 위치 : 클래스, 구조체, 열거형, 프로토콜 및 그 멤버

목적 : 모듈 내부에서만 사용되며, 외부에 노출되지 않아야 하는 코드

ex) 앱 모듈에서만 사용할 목적으로 작성된 코드

```swift
internal class Cat: Animal {
	override internal func bark() {
		printf("야아옹")
	}
}

// 외부 모듈이면 에러
let cat: Cat = Cat() // 에러남
```

</aside>

<aside>

### 4️⃣ fileprivate

특징 : 같은 파일 내에서만 접근 가능

사용 위치 : 클래스, 구조체, 열거형, 프로토콜 및 그 멤버

목적 : 특정 파일 내에서 코드가 상호작용 해야하지만, 다른 파일에는 노출되지 않아야 하는 경우

ex) 클래스의 내부 구현이 같은 파일 내의 다른 클래스를 사용할 때

```swift
fileprivate class Dog {
	fileprivate func bark() {
		printf("멍멍")
	}
}

fileprivate let dog = Dog() // 다른 소스 파일이면 에러남
dog.bark()
```

</aside>

<aside>

### 5️⃣ private

특징 : 같은 선언 내에서만 접근 가능 (즉, 다른 클래스나 구조체에서도 접근 불가)

사용 위치 : 클래스, 구조체, 열거형 및 그 멤버

목적 : 객체의 가장 엄격한 은닉을 유지하려는 경우

ex) 클래스 내부에서만 사용되는 보조 메서드나 프로퍼티

```swift
class Company {
	private let developer = Developer()
	
	func writeCode() {
		developer.writeCode()
	}
}

let company: Company = Company()

company.developer.? // 접근 불가능 에러남
```

</aside>

## 접근 제어자를 사용하는 이유

### 1. 캡슐화

- 객체 내부의 구현 세부 사항을 외부에 숨겨 모듈화 및 유지보수를 용이하게 함
- 내부 구현이 변경되더라도 외부에 영향을 미치지 않도록 보호

### 2. 코드 안정성

- 의도치 않은 접근이나 수정으로부터 보호하여 예기치 않은 오류 방지

### 3. API 설계

- 라이브러리나 프레임워크를 설계할 때, 외부에서 필요한 요소만 노출하고 내부 구현 세부 사항은 감춤

### 4. 보안

- 민감한 데이터를 외부에서 직접 접근하지 못하도록 차단

---

## 접근 제어자 결정 기준 (사용 시기)

### 1. open VS public

- 외부 모듈에서 상속 및 재정의 필요 → open 사용
- 외부에서 접근만 가능하고 변경 불가 → public 사용

### 2. internal

- 모듈 내부에서만 사용되는 경우 (기본값)

### 3. fileprivate

- 같은 파일 내에서 여러 클래스나 구조체 간의 협력이 필요한 경우
    
    : ex) 클래스와 그 확장이 같은 파일에 있는 경우
    

### 4. private

- 특정 클래스나 구조체 내부에서만 사용되도록 제한
    
    ex) 외부 노출이 필요 없는 헬퍼 메소드나 프로퍼티