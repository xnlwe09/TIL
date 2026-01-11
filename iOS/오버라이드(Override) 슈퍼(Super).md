# 오버라이드(Override) / 슈퍼(Super)

생성일: 2025년 8월 20일 오후 10:26

## 오버라이딩(Overriding)

**서브 클래스(자식 클래스)가 슈퍼 클래스(부모 클래스)로부터 상속받은 프로퍼티, 메서드 등을**

**그대로 사용하지 않고 재정의해서 사용하는 것**

<aside>

### 📍메서드 오버라이딩(Method Overriding)

상속받은 인스턴스/타입 메서드를 오버라이딩(Overriding)해서

하위 클래스에서 해당 메서드를 원하는 대로 구현 가능

```swift
class Worker {
    var name: String?
    var position: String?
    
    func introduce() {
        print("My name is \(name ?? "Unknown")")
    }
}

class Developer: Worker {
    var language: String = "Swift"
    override func introduce() {
        print("\(name ?? "Unknown")는 개발자다")
    }
}

let dev = Developer()
dev.name = "주희"
dev.position = "개발자"

dev.introduce() // 주희는 개발자다
```

</aside>

“My name is 주희”와 “주희는 개발자다”를 같이 출력하고 싶을 때

→ 한 번 오버라이딩된 메서드는 오버라이딩 하기 전 메서드로 사용 할 수 없음

그럴 때 오버라이딩 하기 전 메서드를 사용하고 싶으면 직접 슈퍼 클래스의 메서드를 실행 시키면 됨

**= Super를 사용합니당**

<aside>

### 📍Super

Super를 이용하여 슈퍼 클래스에 접근

```swift
class Worker {
    var name: String?
    var position: String?
    
    func introduce() {
        print("My name is \(name ?? "Unknown")")
    }
}

class Developer: Worker {
    var language: String = "Swift"
    
    override func introduce() {
        super.introduce() // 슈퍼 클래스 메서드 실행
        print("\(name ?? "Unknown")는 개발자다")
    }
}

let dev = Developer()
dev.name = "주희"
dev.position = "개발자"

dev.introduce()
// My name is 주희
// 주희는 개발자다
```

</aside>