# Subscribe

생성일: 2025년 10월 28일 오전 12:53

## 개요

그 전까지는 Observable을 정의만 하고 구독을 하지 않았기 때문에 아무런 일도 일어나지 않음 !

Subscribe를 통해 구독하는 법을 알아봅시당당

```swift
func subscribe(_ on: @escaping (Event<Element>) -> Void) -> Disposable // 반환 타입
```

on 뒤에 있는 클로저를 보면 Event 타입을 받아서 어떠한 일을 할 수 있도록 만들어줌

→ 각각의 이벤트 타입 next, error, completed 에 대해 어떤 일을 해줄지 정의해줄 수 있다

```swift
Observable.of(1,2,3) // 옵저버블 생성
    .subscribe(onNext: { num in
        print(num)
    }, onCompleted: {
        print("completed")
    })

// 출력
// 1
// 2
// 3
// completed
```

## 이벤트

<aside>

### 📍onNext:

Observable이 새로운 항목을 방출할 때마다 이 클로저가 호출됨

이때 Observable이 방출하는 클로저의 파라미터로 전달받음

</aside>

<aside>

### 📍onError:

Observable은 기대하는 데이터가 생성되지 않았거나 다른 이유로 오류가 발생했을 때,

이 오류를 구독자인 Observer에게 알리기 위해 이 메서드를 호출함

</aside>

<aside>

### 📍onCompleted:

Observable은 이벤트가 종료되어 더이상 호출되지 않을 때,

이벤트가 완료 되었음을 구독자인 Observer에게 알리기 위해 이 메서드를 호출함

</aside>

## Disposing (구취하기)

Disposable → 구독을 취소할 수 있는 클래스

subscribing은 Observable이 이벤트를 방출하도록 해주는 방아쇠 역할을 하고,

이벤트를 가지고만 있던 Observableadp subscribe 메서드를 사용하면

return 값으로 Disposable한 객체를 만들어줌

→ 언제든 구독을 취소할 수 있는 가능성이 열려있다 !

Disposable한 객체이기 때문에 dispose()를 통해서 구독을 버릴 수 있음

### 근데 왜 버려욤 🗑️

→ Observable은 관측 가능한 이벤트의 흐름을 내보내는 것이고, 이 흐름을 구독하여 특정 이벤트에 대한

처리를 해줄 수 있음 하지만 말 그대로 구독을 하고 있는 상태이기 때문에 구독만 하고 취소하지 않으면 메모리 누수가 발생하게 되기 때문에 이를 방지하기 위해 dispose 해서 버려주는 것 (구독 취소)

<aside>

### 📍dispose

```swift
subscription.dispose()
// disposable한 인스턴스를 생성해서 원하는 시점에 dispose 할 수 있고
```

```swift
.dispose()
// 그냥 원하는 시점에 dispose 할 수도 있음
```

</aside>

<aside>

### 📍Disposebag

구독을 DisposeBag에 넣어서 나중에 한꺼번에 해제되게 하는 것

하나씩 적절한 시점에 다 구독 취소하기엔 귀찮기 때문에 쓰레기통과 같은 DisposeBag을 사용

```swift
let disposeBag = DisposeBag()

Observable.of("A", "B", "C")
  .subscribe { print($0) }
  .disposed(by: disposeBag)

Observable.of("A", "B", "C")
  .subscribe { print($0) }
  .disposed(by: disposeBag)

Observable.of("A", "B", "C")
  .subscribe { print($0) }
  .disposed(by: disposeBag)
```

disposeBag에 Disposable 인스턴스들을 disposed(by:) 메서드로 넣어주면

disposeBag이 메모리에서 해제될 때 모든 구독이 취소됨

ex) VC에 disposeBag를 선언하고, 여러가지 Observable에 대한 disposable을

disposeBag에 넣어주면 VC가 메모리에서 해제될 때 구독도 모두 취소가 되는 것!

</aside>

조금 더 쉽게 말하자면

subscribe의 반환값은 disposable이기 때문에 그 반환값을 disposeBag에 넣음

→ 그 뒤 diseposeBag이 deinit(메모리에서 해제)될 때 그 안에 들어있던 모든 disposable들의 dispose()가 자동 호출되면서 구독 취소가 됨