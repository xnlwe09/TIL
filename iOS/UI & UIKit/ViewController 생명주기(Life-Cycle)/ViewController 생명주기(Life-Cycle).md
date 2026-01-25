# ViewController 생명주기(Life-Cycle)

## ViewController의 생명주기란?

ViewController가 생성되고 사라지는 등 View의 상태와 관련된 과정

(화면이 전환되는 시점에 호출되는 함수들)

![image.png](ViewController%20%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0(Life-Cycle)/image.png)

![image.png](ViewController%20%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0(Life-Cycle)/image%201.png)

<aside>

### 📍init

ViewController 인스턴스가 생성될 때 호출

ViewController 인스턴스가 메모리에 생성되는 시점에 호출되며,
필수 프로퍼티 초기화 및 의존성 주입을 담당

</aside>

<aside>

### 📍loadView

`viewDidLoad` 이전에 호출되어 View를 만들고 이를 메모리에 올리는 역할

(애플 왈 : 이 메서드는 직접 호출하지 마셈)

</aside>

<aside>

### 📍viewDidLoad

View가 메모리에 올라온 후 한 번만 호출
(View가 메모리에서 해제된 후 다시 메모리에 올라오면 다시 호출될 수 있음)

시스템에 의해 자동으로 호출되기 때문에 일반적으로 리소스를 초기화하거나 초기 화면 구성 용도로 사용

</aside>

<aside>

### 📍viewWillAppear

View가 화면에 나타나기 전 호출

메모리와 상관없이 현재 화면이 해당 View가 보이는지에 대해서만 영향을 받기 때문에
메모리에 올라온 후 한 번만 호출되는 `viewDidLoad`와 다르게 View가 화면에 나타나기 직전마다 호출됨

</aside>

<aside>

### 📍viewDidAppear

View가 화면에 나타난 직후 호출
(ViewController가 View 계층 구조에 추가된 직후)

View가 화면에 나타났음을 ViewController에 알리는 시점이며, 화면 전환 애니메이션이 완료된 이후 호출

</aside>

<aside>

### 📍viewWillDisappear

View가 사라지기 직전 호출

ViewController의 View가 화면에서 내려가기 직전 시점을 알려줌

</aside>

<aside>

### 📍viewDidDisappear

View가 화면에서 사라진 직후 호출

(View가 화면에서 사라진 것 뿐, 메모리에서 해제된 것은 아님)

</aside>

<aside>

### ⛔️ viewDidUnload

iOS 5 이전에는 메모리 경고 시 View가 unload될 수 있었고
이 메서드를 통해 View에 대한 참조를 해제할 수 있었지만
iOS 6 이상부터 View unloading이 제거되면서 deprecated 되어 사용이 중단됨

이후 메모리 경고에 대한 처리는 `didReceiveMemoryWarning()`에서 수행하며,
이 메서드에서는 View 자체를 해제하기 보다 View와 관련된 캐시나
불필요한 리소스를 정리하는 용도로 사용됨

</aside>