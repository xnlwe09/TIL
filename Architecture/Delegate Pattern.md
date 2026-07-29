# Delegate Pattern

## Delegate Pattern이란?

객체 간의 통신을 구현하는 데 사용되는 디자인 패턴으로, 한 객체가 다른 객체에게 작업의 처리를 위임할 때 사용
(특정 객체에서 이벤트나 작업이 발생했을 때 그 처리 방법을 다른 객체(Delegate)에 위임하는 방식)

### 역할

- A 객체가 특정 이벤트나 작업을 처리할 권한을 B 객체에게 위임(delegate)
- 위임받은 객체는 정의된 프로토콜을 준수하여 해당 작업을 수행

### 주요 특징

**1:1 관계** - 한 객체는 일반적으로 하나의 delegate만 가짐

**타이트한 결합** - 위임받은 객체를 명시적으로 지정해야 함

**유연성** - 이벤트나 작업 처리 로직을 외부 객체에 위임하여 재사용성과 코드 분리를 향상

## Delegate Pattern 사용 사례

Delegate Pattern은 1:1 이벤트 처리가 필요한 상황에서 사용됨

1. UITableView, UICollectionView
- 데이터 소스와 사용자 인터랙션 처리를 UITableViewDelegate, UITableViewDataSource
2. 커스텀 뷰의 이벤트 처리
- 사용자 정의 UI 요소가 특정 동작을 다른 객체에 위임할 때
3. 비동기 작업 결과 전달
- 네트워크 요청의 결과를 호출한 객체로 전달
(현재는 Closure나 async/await을 더 많이 사용)

## Delegate Pattern, Notification, KVO 차이점

모두 객체 간 통신을 위한 패턴!!

<aside>

### 📍Delegate Pattern

**1:1 관계에서 사용**
이벤트를 명확히 정의된 프로토콜을 통해 전달

장점
- 명확한 구조와 강한 타입 안정성

단점
- 위임 객체를 명시적으로 설정해야 함
- 객체 간 결합도가 높아질 수 있음

</aside>

<aside>

### 📍Notification(NSNotificationCenter)

**1:N 관계에서 사용**
앱 전체에 이벤트를 방송(Broadcast)하여 여러 객체가 이를 수신

장점
- 느슨한 결합(loose coupling)
- 이벤트를 전역적으로 관리 가능

단점
- 이벤트 관리가 복잡해질 수 있음
- 수신 대상이 명시적이지 않음

</aside>

<aside>

### 📍KVO (Key-Value Observing)

**특정 객체의 속성 값이 변경되었을 때 이를 감지**
객체 간 결합 없이 상태 변화를 관찰

장점
- 상태 변경 감지에 적합

단점
- Objective-C 기반의 구현
- Swift에서는 Combine, Observation, ObservableObject 등의 현대적인 방식이 많이 사용됨

</aside>

## Delegate Pattern 구현 방법

구현 단계

1. 프로토콜 정의
- Delegate가 수행해야할 동작을 정의
2. Delegate 속성 선언
- 작업을 위임할 객체를 참조하는 속성
3. Delegate 호출
- 특정 이벤트가 발생했을 때 delegate 메서드 호출

```swift
// 1. 프로토콜 정의
protocol MyDelegate: AnyObject {
    func didReceiveData(_ data: String)
}
 
// 2. 작업 위임 객체 (Sender)
class Sender {
    weak var delegate: MyDelegate? // Delegate 속성 선언
    
    func performTask() {
        let data = "Hello, Delegate!"
        delegate?.didReceiveData(data) // Delegate 호출
    }
}
 
// 3. Delegate 구현 객체 (Receiver)
class Receiver: MyDelegate {
    func didReceiveData(_ data: String) {
        print("Data received: \(data)")
    }
}
 
// 4. 사용 예
let sender = Sender()
let receiver = Receiver()
sender.delegate = receiver // Delegate 설정
 
sender.performTask() // "Data received: Hello, Delegate!"

```

## Delegate Pattern에서 주의할 점

Delegate Pattern을 사용할 때는 Strong Reference Cycle(강한 순환 참조)를 주의해야 함

두 객체가 서로를 강하게 참조하면 둘 중 하나가 더이상 필요하지 않더라도
메모리에서 해제되지 않아 메모리 누수(Memory Leak)가 발생할 수 있음

### 왜 Strong Reference Cycle이 발생할까

- Delegate Pattern을 구현할 때, 위임자(Delegator)가 delegate 프로퍼티를 통해 Delegate 객체를 참조
- 반대로 Delegate 객체도 위임자를 강한 참조(ex 프로퍼티)를 통해 보유하고 있는 경우 강한 순환 참조 발생

### 해결 방법

1. Delegate 프로퍼티를 weak로 선언
- Delegate 프로퍼티를 weak로 선언하면 참조 카운트가 증가하지 않아 순환 참조를 방지할 수 있음

```swift
protocol MyDelegate: AnyObject {
    func didPerformAction()
}
 
class AViewController: UIViewController {
    weak var delegate: MyDelegate? // weak 선언
}
```

1. 중재 객체를 사용하여 간접적으로 연결
- Delegate 역할을 담당하는 별도의 객체를 생성하여 순환 참조를 방지
2. unowned 사용
- 특정 상황에서 Delegate 객체가 항상 위임자보다 더 오래 살아있을 것이 확실한 경우 사용 가능

```swift
unowned var delegate: MyDelegate
```

but Delegate 객체가 먼저 해제될 가능성이 있다면, 런타임 에러가 발생할 수 있으니 신중하게 사용해야함