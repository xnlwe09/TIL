# MVVM (디자인 패턴)

![image.png](MVVM%20(%EB%94%94%EC%9E%90%EC%9D%B8%20%ED%8C%A8%ED%84%B4)/image.png)

## MVVM이란?

Model-View-ViewModel 로 나누어 코드를 관리하는 방식

<aside>

### 1️⃣ Model

- 데이터를 다루는 계층
    - 데이터를 담아두기 위한 구조체(Entity, DTO 등)
    - 네트워크 통신
    - JSON 파싱
    - 데이터 저장 및 관리(DB, UserDefaults)
- View, ViewModel에 전혀 의존하지 않음 → 재사용성 극대화
    - 앱에서 다루는 데이터 자체에만 신경 쓰면 됨
</aside>

<aside>

### 2️⃣ View

- UI를 구성하고 화면에 표시하는 계층
- View의 각 컴포넌트(UI 요소)와 레이아웃을 정의
- 버튼, 라벨, 이미지 등의 화면 요소 표시
- 사용자의 입력(터치, 스크롤, 입력 등)을 ViewModel에 전달
- ViewModel을 참조하며, Model은 직접 접근 금지
    - ViewModel이 제공하는 데이터를 화면에 표시하는 방식
- 재사용성이 강조되며, 컴포넌트를 적당히 잘 나누어 중복된 코드를 줄이는 것이 중요
</aside>

<aside>

### 3️⃣ ViewModel

- View의 요청을 받아 Model을 통해 데이터를 처리하고, 그 결과를 View에 제공하는 계층
    - View와 Model 사이의 중개자 역할
- 화면에 필요한 데이터를 가공하고 비즈니스 로직을 수행
- View가 사용할 데이터(데이터 바인딩 대상)를 제공
- Model의 데이터가 변경되면 View가 화면을 갱신할 수 있도록 변경 사항을 전달
</aside>

## MVVM 특징

<aside>

### 📍장점

- View와 비즈니스 로직이 분리되어 테스트와 유지보수가 용이
- ViewModel의 로직을 재사용하여 여러 View에서 활용할 수 있음
- ViewModel이 데이터 가공 담당 → View 단순화, 코드가 깔끔함
- 데이터 바인딩을 적용하면 데이터 변경 시 UI를 효율적으로 갱신할 수 있음
</aside>

<aside>

### 📍단점

- 설계가 어려움
- ViewModel이 비대해질 수 있음
- 데이터 바인딩을 적용하면 데이터 흐름이 복잡해져 디버깅이 어려워질 수 있음
</aside>

## MVC와 MVVM의 차이

<aside>

### 📍MVC

- Model : 비지니스 데이터와 로직
- View : UI를 구성하고 화면에 표시하는 계층
- Controller : View와 Model 연결 (사용자의 입력을 처리하고 Model과 View를 연결하며 화면 갱신)

Controller가 View와 Model 모두를 다룸 → 두 레이어가 강하게 연결

그래서 규모가 커질수록 Controllerr 코드가 비대해짐 (Massive ViewController 문제)

View와 Controller의 결합도가 높아 Controller의 재사용이 어렵고 유지보수가 어려움

</aside>

<aside>

### 📍MVVM

- Model : 비지니스 데이터와 로직
- View : UI 정의 및 사용자 이벤트 수신
- ViewModel : 비즈니스 로직과 데이터 가공, View가 사용할 데이터(바인딩 대상) 제공
    - 데이터 바인딩 : 데이터와 UI를 연결하여 동기화하는 것

데이터 바인딩을 통해 View와 ViewModel의 데이터를 동기화

ViewModel은 View를 직접 알지 않음 → View와의 결합도가 낮음

ViewModel의 로직을 재사용할 수 있어 코드 중복을 줄일 수 있음

View는 화면 표시에만 집중, 로직은 ViewModel로 이동 → UI 코드 단순화

</aside>

## 왜 MVC 말고 MVVM을 쓸까?

<aside>

### 1. 관심사의 분리 (Separation of Concerns)

- MVC : View와 Controller가 서로 강하게 연결되어 역할이 명확하게 분리되지 않음
- MVVM : View와 비즈니스 로직을 ViewModel로 분리하여 각 계층의 역할이 명확하고 결합도가 낮음

### 2. 테스트 용이성

- MVC : Controller와 UI가 강하게 연결되어 있어 단위 테스트가 어려움
- MVVM : ViewModel은 UI와 독립적 → 단위 테스트 쉬움

### 3. 재사용성

- MVC : Controller는 특정 View와 강하게 결합되어 재사용이 어려움
- MVVM : ViewModel의 로직을 여러 화면에서 재사용할 수 있어 코드 중복을 줄일 수 있음

### 4. 확장성

- MVC : 프로젝트 규모가 커질수록 Controller가 비대해져 유지보수가 어려워짐
- MVVM : 로직을 ViewModel로 분리하여 기능 추가와 유지보수가 용이
</aside>

MVC는 단순하고 빠른 개발에 유리하지만, 규모가 커지면 Controller가 비대해지고 유지보수가 어려움

MVVM은 초기 구조 설계가 MVC에 비해 복잡하지만, 관심사 분리, 테스트 용이성, 재사용성, 확장성 측면에서 유리

→ 꼭 UIKit와 SwiftUI의 차이 때문이 아니라도 프로젝트의 규모가 커질 때도 유지보수성과 확장성을 확보하기 위해 MVVM을 사용하기도 함