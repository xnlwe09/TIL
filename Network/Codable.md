# Codable

## Codable이란?

외부 표현으로 변환(Encode)하거나 외부 표현으로 부터 변환(Decode)할 수 있도록 하는 프로토콜
Encodable & Decodable로 구성

> Codable을 채택했다 = Class, Struct, Enum을 Encoding(직렬화) / Decoding(역직렬화) 할 수 있다
> 

## Encoding / Decoding

<aside>

### 📍Encoding (Encodable)

Class, Struct, Enum 등의 인스턴스를 JSON 형태의 Data로 만들어주는 것

```swift
struct Human: Codable {
	var name: String
	var age: Int
}

let juhui: Human = .init(name: "Juhui", age: 18) // 구조체 변수 생성

let data = try? JSONEncoder().encode(juhui) // Encoding !!
```

</aside>

<aside>

### 📍Decoding (Decodable)

JSON 형태의 Data를 Class, Struct, Enum 등의 인스턴스에 자동으로 파싱

```swift
struct Human: Codable {
	var name: String
	var age: Int
}

let data = """
{
    "name" : "Juhui",
    "age"  : 18
}
""".data(using: .utf8)! // 서버에서 준 JSON 데이터 예시

let juhui = try? JSONDecoder().decode(Human.self, from: data)
// Human 구조체 변수에 Decoding !!
```

Human 타입의 구조체를 하나 만들고, JSON Data의 Key 값과 동일한 이름의 구조체 변수에
value 값을 파싱 → 파싱된 구조체를 리턴

즉, JSON Data의 Key 값은 Codable을 따르는 타입(Human 구조체)의 프로퍼티 이름과
1:1 매칭이 되어야만 문제 없이 사용 가능 (다를 경우 CodingKey를 사용해 매핑)

</aside>

## CodingKey

JSON 데이터의 Key 값과 모델의 프로퍼티 이름이 다를 때,
Encoding / Decoding 과정에서 두 이름을 매핑하기 위해 사용하는 프로토콜

```swift
struct Human: Codable {
	var name: String

	enum CodingKeys: String, CodingKey {
		case name = "Name"
	}
}
```

JSON Key인 `Name`과 Swift 프로퍼티인 `name`을 매핑하도록 정의

## Optional Key

Key-Value 쌍 자체가 존재하지 않는 경우

<aside>

#### 📍프로퍼티를 Optional로 선언

JSON에 해당 Key가 없을 경우 프로퍼티를 Optional로 선언하여 Decoding 실패를 방지

```swift
struct Human: Codable {
	var name: String?
}
```

</aside>

<aside>

#### 📍`init(from: )` 을 직접 구현해 기본값 지정

Key가 없을 때 특정 기본값을 사용하고 싶다면 `init(from decoder: Decoder)` 를
직접 구현하여 원하는 기본값으로 대체할 수 있음

</aside>

<aside>

- 없어도 되는 데이터 → `String?`
- 없으면 안 되는 데이터 → `String`
- 없어도 되지만 앱 내부에서는 기본값이 필요한 데이터 → `init(from:)` 활용
</aside>

## Nullable

특정 Key의 Value가 null인 경우

<aside>

#### 📍프로퍼티를 Optional로 선언

JSON에 특정 Key의 Value가 null일 경우 프로퍼티를 Optional로 선언하여 Decoding 실패를 방지

```swift
struct Human: Codable {
	var name: String?
}
```

</aside>