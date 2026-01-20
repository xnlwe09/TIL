# 에러 처리(Error Handling)

## 에러 처리(Error Handling)란?

프로그램의 오류 조건에 대응하고 복구하는 과정

## Swift의 에러 처리 방법

Swift에서는 안전하고 명시적인 방식으로 에러를 처리하기 위해 에러 처리 기능을 제공

Swift의 에러 처리는 에러를 발생(throw), 전파(throws), 처리(catch)하는 방식을 기반으로 함

---

열거형으로 에러를 그룹화 (Error 프로토콜을 채택합니당)

```swift
enum AppError: Error {
    case invalid
    case failed
}
```

<aside>

### throws

에러를 발생시킬 가능성이 있는 함수나 메서드에 사용 (아직 에러 발생은 안 함)

throws를 선언한 함수는 호출할 때 반드시 try 키워드 사용

값 반환을 한다면 `throws → 타입`

```swift
func validate(_ value: Int) throws {
    if value < 0 {
        throw AppError.invalid
    }
}
```

</aside>

<aside>

### throw

실제로 에러를 던짐

```swift
throw AppError.invalid // AppError에 있는 invalid 케이스
```

</aside>

<aside>

### try

throws 함수 호출 시 사용하며, 에러가 발생할 가능성을 명시적으로 나타냄

- try : 에러가 발생하면 현재 스코프에서 처리하거나, 처리하지 않으면 상위 호출자로 전파
- try? : 에러를 옵셔널 값으로 변환 (실패 시 nil)
- try! : 에러를 무시하고 강제로 실행(런타임 크래시⚡️)

### catch

do 블록에서 발생한 에러를 처리

패턴 매칭을 활용하여 특정 에러 유형을 구분 가능

```swift
do {
    try validate(-1)
    print("성공")
} catch AppError.invalid {
    print("잘못된 값")
}
```

</aside>

---

책임을 넘긴다고 선언하는 건

```
throws
```

실제로 넘기는 건

```
throw
```

넘겨받는 건

```
try
```