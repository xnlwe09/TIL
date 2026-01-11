# Swift(iOS) MVC (디자인패턴)

생성일: 2025년 8월 20일 오후 10:26

![image.png](Swift(iOS)%20MVC%20(%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4)%20255933c2941a81a88dffc1672cd9df30/image.png)

## MVC란?

Model-View-Controller의 약자로 Application을 세 가지 역할로 나누어 관리하는 디자인 패턴

<aside>

### 1️⃣ Model

- 데이터와 비즈니스 로직 담당
    - 앱에서 다룰 데이터를 어떤 형태로 저장하고 다룰지 결정 →데이터의 타입과 속성을 설계하는 과정
- UI와 직접적으로 연결되지 않음
- 데이터 처리, DB 관리
    - 데이터 저장/조회 가능, 어디서 저장할지, 어떻게 가져올지와 관련된 로직 포함 가능

(지피티 왈 : API 호출 - 전통 MVC에서는 Controller, 실무에서는 Model에 넣기도 함)

</aside>

<aside>

### 2️⃣ View

- 사용자에게 보여지는 화면(UI)과 관련된 요소 담당
- UILabel, UIButton, UIImageView 같은 UIKit 객체 포함
- 데이터를 표시하지만 데이터를 직접 처리하진 않음
</aside>

<aside>

### 3️⃣ Controller

- Model과 View를 연결해주는 역할
- View에서 보여주기 위한 데이터를 Controller가 보내서 View를 refresh하고
    
    그 데이터를 Model으로부터 가져옴
    
</aside>

## 🍎 Apple의 MVC

View와 Controller를 ViewController 하나로 취급

## Swift 관점의 MVC 흐름

<aside>

### 📍Controller to View/Model

- View: Outlet을 통해 직접 접근 가능
- Model: Controller가 직접 접근하여 데이터 가져오기 / 수정 가능
</aside>

<aside>

### 📍View to Controller

- Target-Action 구조 : 사용자의 이벤트에 따라 함수 호출
- Delegate / DataSource: 미리 정해진 방식으로 요청 처리 가능
</aside>

<aside>

### 📍Model to Controller

Model은 데이터와 로직만 담당, UI나 Controller 구조에는 전혀 신경 쓰지 않음

Model 쪽에 있는 코드는 데이터를 제공하는 코드라

위에 있는 Controller가 어떻게 만들어져있는지는 아예 모르는 구조이기 때문에, 직접 접근은 불가능

→ Notification & KVO(Key-Value Observing) 방식을 통해 Model의 변화를 Controller에 알릴 수 있음

→ Model이 데이터가 바뀌었음을 알릴 필요가 있을 때 사용

</aside>

## MVC 특징

<aside>

### 📍장점

- 구조가 간단하고 직관적 → 작은 프로젝트에서의 빠른 개발 가능
- Apple에서 기본적으로 지원하고 있는 패턴이기 때문에 쉬운 개발 가능
</aside>

<aside>

### 📍단점

- View와 Controller의 강한 결합
    - Controller가 View의 Lift Cycle까지 관리
        
        → View와 Controller의 분리가 어렵고 재사용성이 떨어짐
        
- 거대한 ViewController(Massive View Controller)
    - Life Cycle 관리, delegate, datasource, 네트워크 요청 등 많은 코드가 Controller에 작성됨
        
        → Controller의 크기가 커지고 내부 구조가 복잡해짐
        
        → 프로젝트 규모가 커질수록 유지보수 어려움
        
</aside>