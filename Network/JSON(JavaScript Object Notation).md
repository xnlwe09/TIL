# JSON(JavaScript Object Notation)

## JSON(JavaScript Object Notation)이란?

데이터를 교환하고 저장하기 위한 텍스트 기반의 데이터 표현 형식

### 기본 구조

키(Key)와 값(Value)의 쌍

```json
{ "key": "value" }

{
    "key": "value",
    "key2": "value2"
} // 여러 데이터를 나열할 경우

{
    "user": {
        "name": "홍길동"
    },
    "friends": [
        "철수",
        "영희",
        "민수"
    ]
}
// 객체(Object)는 중괄호 {}
// 배열(Array)는 대괄호 []
```

### JSON 문법 규칙

- Key는 반드시 큰따옴표(`"`)로 감싼 문자열
- 문자열(String)은 반드시 큰따옴표 사용
- 마지막 요소 뒤에는 쉼표(`,`)를 붙일 수 없음
- 객체는 `{}`
- 배열은 `[]`

### JSON은 어디에 사용될까?

- REST API 요청(Request)
- REST API 응답(Response)
- 설정 파일(Configuration)
- 데이터 저장 및 교환

## JSON과 API 통신

서버와 클라이언트는 데이터를 JSON 형태로 주고받음

### Server → Client

```json
{
    "id": 1,
    "title": "게시글 제목",
    "content": "내용"
}
```

### Client(iOS)

JSON 데이터를 앱에서 사용할 수 있는 객체 형태로 변환하여 사용

(Swift에서는 Codable을 활용해 JSON 데이터와 객체를 변환할 수 있음)

```swift
struct Post: Codable {
    let id: Int
    let title: String
    let content: String
}
```

## Serialization / Deserialization

데이터 형식을 변환하는 과정

<aside>

### 📍Serialization(직렬화)

객체 → JSON 데이터

```smalltalk
객체(Object)
      ↓
JSON 데이터
```

데이터를 저장하거나 서버에 데이터를 보낼 때 사용

</aside>

<aside>

### 📍Deserialization(역직렬화)

JSON 데이터 → 객체

```smalltalk
JSON 데이터
 ↓
객체(Object)
```

서버에서 받은 데이터나 저장된 데이터를 객체 형태로 사용할 때 사용

</aside>