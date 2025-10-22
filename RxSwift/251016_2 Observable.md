# Observable

생성일: 2025년 10월 15일 오후 2:21

## Observable이란?

관찰이 가능한 흐름으로, 비동기 이벤트가 발생했을 때 항복(item)들을 **시퀀스**로 방출하는 대상

**RxSwift는 반응형 프로그래밍이기 때문에 어떤 비동기 이벤트에 대해 관찰 가능한 형태(Observable)로 만듦**

비동기 이벤트를 어떤 관찰 가능한 형태로 만든다는 것

= 비동기 이벤트를 제네릭 타입의 Observable이란 클래스 인스턴스를 만든다는 것

```swift
public class Observable<Element> : ObserbableType {
```

Observable은 제네릭 클래스로 구성 되어 있음 (어떤 타입의 데이터든 시퀸스로 방출할 수 있어야하기 때문에)

### 시퀀스(Sequence)란?

Observable이 방출하는 이벤트들의 흐름

<aside>

🌟 비동기 이벤트에 대한 Observable은 비동기 이벤트가 발생했을 때

해당 이벤트가 발생했다는 것을 알려주기 위해 **항목(item)을 시퀀스(Sequence)로 방출(emit)함**

</aside>

버튼이 여러번 눌리면 그만큼 Observable은 해당 이벤트에 대한 항목을 순서대로 방출

```swift
button.rx.tap
    .subscribe(onNext: {
        print("버튼 클릭!")
    })
```

<aside>

### ex) 버튼 클릭 이벤트

Rx = 데이터의 흐름이 변경되었을 때 전파하는 데 중점을 둔 프로그래밍

→ 데이터 = 버튼

→ 데이터의 흐름 변경 → 버튼 클릭

즉, 이 버튼의 흐름 변경을 전파하기 위해선 버튼의 클릭 이벤트가

“관찰이 가능한 형태”인 Observable이 되어야하는 것 ! 그것을 RxSwift가 할 수 있다~

그리고 이벤트가 일어났을 때 이를 알리기 위해 그 이벤트에 대한 항목을 시퀀스로 방출

</aside>