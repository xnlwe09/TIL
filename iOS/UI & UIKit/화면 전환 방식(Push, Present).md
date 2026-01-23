# 화면 전환 방식(Push, Present)

# Present

### (1) present : 뷰 이동

- 뷰 전환 방식 : 모달 화면 전환
- modalPresentationStyle로 화면 전환이 되는 스타일을 정할 수 있음
- `present(_:animated:completion:)`
    - view controller를 모달 방식으로 보여줌
    - viewControllerToPresent : 전환 될 뷰
    - animated : 애니메이션 여부
    - completion : 이동하고 나서 실행될 문장 블럭

### (2) dismiss : 돌아가기

- present된 뷰(모달)를 메모리에서 삭제하고 걷어냄
- `dismiss(animated:completion:)`
    - animated : 애니메이션 여부
    - completion : 이동하고 나서 실행될 문장 블럭

<aside>

### 📍특징

- 사용자의 이목을 끌기 위한 화면 전환 기법
- 화면을 다른 화면 위로 띄워 표현하는 방식
- 흐름을 이어지는 컨텐츠를 담기 보다는 흐름을 끊고 눈에 보여줘야하는 콘텐츠를 담는데 사용
- present와 dismiss는 UIViewController를 상속받은 화면에서만 가능
- 주로 X 버튼이 있음

</aside>

# Push

### (1) push : 뷰 이동

- 뷰 전환 방식 : 화면 전환
- 스택에 뷰를 쌓는 형태로 화면을 업데이트
- pushViewController(_:animated:)
    - viewController : 전환될 뷰
    - animated : 애니메이션 효과

### (2) pop : 돌아가기

- 스택에 쌓인 뷰 1개를 pop하고 돌아가기
- `popViewController(animated:)`
    - animated : 애니메이션 효과

### (3) popTo : 원하는 스택으로 돌아가기

- 네비게이션 스택의 원하는 ViewController로 돌아가기
    
    (= 특정 viewController가 navigation stack의 맨 위에 올 때까지 Pop)
    
- `popToRootViewController(_:animated:)`
    - viewController : pop해서 이동할 뷰
    - animated : 애니메이션 효과

### (4) popToRoot : 맨 처음으로 돌아가기

- 네비게이션 스택의 RootView로 돌아가기
- popToViewController(_:animated:)
    - animated : 애니메이션 효과

<aside>

### 📍특징

- 계층적 구조의 뷰 워크플로우를 구현하기 위해 사용
- UINavigationController가 여러 UIViewController를 스택 구조로 관리
- Present 방식과 달리, 자식 뷰는 스택으로 관리됨
- Push와 Pop 관련 동작은 항상 NavigationController 환경 안에서 이루어짐
- 주로 < 버튼이 있음
</aside>