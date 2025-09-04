# App/Scene Delegate

생성일: 2025년 8월 20일 오후 10:26

## 개요

**AppDelegate와 SceneDelegate 클래스는 각각 다른 책임을 가지며, 앱의 생명주기 및 상태 관리를 처리한다.**

## AppDelegate

**AppDelegate는 iOS 버전에 상관없이 앱의 진입 지점(entry point) 역할을 하며, 앱 전체 수준(application level)의 생명 주기(life-cycle)** `ex 앱 실행, 종료, 백그라운드·포그라운드 전환` **를 관리한다.**

(iOS 12 이하에서는 모든 백그라운드·포그라운드 전환 이벤트를 AppDelegate가 처리했지만,

iOS 13 이상에서는 앱 전체 단위의 전환 이벤트는 AppDelegate가, 개별 화면(Scene) 단위의 전환 이벤트는 SceneDelegate가 처리한다.)

## AppDelegate 주요 수행작업

<aside>

- **앱 초기화**: 앱이 시작될 때 초기 설정을 처리
- **푸시 알림 설정**: 푸시 알림을 설정하고 처리
- **백그라운드 작업**: 앱이 백그라운드로 전환될 때 필요한 작업 수행
</aside>

## AppDelegate 앱 생명주기(App’s Life Cycle) Method

앱이 시작, 종료, 백그라운드/포그라운드 전환 등 앱 전체의 상태 변화를 알림받아

필요한 초기화, 데이터 저장, 작업 중단/재개 등의 처리를 수행할 수 있다.

<aside>

### 📍application(_:didFinishLaunchingWithOptions:)

앱 실행 직후, 초기화 작업 수행 (가장 먼저 호출되는 진입 지점 메서드)

</aside>

<aside>

### 📍applicationWillResignActive(_:)

앱에 활성 상태에서 비활성 상태로 전환되기 직전 호출

ex) 전화 수신, 홈 화면 전환

</aside>

<aside>

### 📍applicationDidEnterBackground(_:)

앱이 백그라운드로 들어갔을 때 호출

(데이터 저장, 작업 중단 등을 구현할 수 있음)

</aside>

<aside>

### 📍applicationWillEnterForeground(_:)

앱이 백그라운드 → 포그라운드로 가기 직전 호출

</aside>

<aside>

### 📍applicationDidBecomeActive(_:)

앱이 활성 상태가 되었을 때 호출

(UI 업데이트, 일시정지된 작업 재개 구현할 수 있음)

</aside>

<aside>

### 📍applicationWillTerminate(_:)

앱이 완전히 종료되기 직전 호출

(사용자 데이터 저장, 캐시 정리, 네트워크 연결 종료 등을 구현 가능)

</aside>

*iOS에서는 강제 종료(사용자가 앱 스와이프)나 시스템이 앱을 종료할 땐

applicationWillTerminate(_:)가 호출되지 않을 수 있음

→ 따라서 중요한 데이터 저장은 applicationDidEnterBackground(_:)에서 처리하는 것이 안전

applicationDidEnterBackground(_:)

- 앱이 백그라운드로 갈 때 호출
- 가장 안전한 시점: 사용자가 앱을 강제로 종료하거나 시스템이 앱을 종료해도 이 메서드는 호출됨
- 그래서 중요한 사용자 데이터는 이 시점에 저장하는 걸 권장

applicationWillTerminate(_:)

- 앱이 정상적으로 종료될 때 호출
- 하지만 사용자가 앱을 스와이프해서 종료하거나, 시스템이 강제로 종료하면 호출되지 않을 수 있음
- 여기에만 의존하면 데이터 유실 위험이 있음

중요 데이터 저장 → applicationDidEnterBackground(_:)에서

applicationWillTerminate(_:) → 추가 정리용, 보조 역할 정도

## SceneDelegate

**SceneDelegate는 iOS 13 이후로 도입된 클래스이며, 앱의 각 장면(Scene)에 대한 생명주기를 관리한다.**

**멀티 윈도우 환경을 지원하기 위해 도입되었고 앱이 여러 UI 창을 가질 수 있는 경우 각 창의 상태를 독립적으로 관리한다.**

## SceneDelegate 주요 수행작업

<aside>

- **UI 상태 관리**: 각 장면의 UI 상태를 관리
- **장면 생명주기 이벤트 처리**: 장면이 활성화되거나 비활성화될 때 이벤트를 처리
</aside>

## SceneDelegate 장면(Scene) 생명주기 Method

각 화면이 활성화, 비활성화, 포그라운드/백그라운드 전환될 때 호출되어

화면 단위의 상태를 관리하고 필요한 작업을 수행할 수 있다.

<aside>

### 📍scene(_:willConnectTo:options:)

장면이 앱에 연결될 때 최초로 호출

(보통 UI 초기화, 윈도우 설정 등을 이곳에서 수행)

ex) window = UIWindow(windowScene: scene as! UIWindowScene)

</aside>

<aside>

### 📍sceneDidDisconnect(_:)

장면이 앱에서 분리될 때 호출

(시스템에서 장면(Scene)이 곧 해제될 예정이라는 신호를 보내는 거임)

(개발자는 리소스 해제, 장면 관리 객체 정리 등을 할 수 있음)

</aside>

<aside>

### 📍sceneDidBecomeActive(_:)

장면이 활성 상태가 되었을 때 호출

(UI 업데이트, 일시정지된 작업을 재개할 수 있음)

</aside>

<aside>

### 📍sceneWillResignActive(_:)

장면이 비활성 상태로 전환될 때 호출

(처리 방법 ex) 타이머 일시정지, 작업 중단 등)

</aside>

<aside>

### 📍sceneWillEnterForeground(_:)

장면이 백그라운드 → 포그라운드로 돌아가기 직전 호출

(장면이 다시 사용자에게 보여지기 전에 UI를 최신 상태로 준비하고, 필요한 상태 정보를 갱신)

</aside>

<aside>

### 📍sceneDidEnterBackground(_:)

장면이 포그라운드 → 백그라운드로 들어갔을 때 호출

(장면이 더 이상 사용자에게 표시되지 않을 때 중요 데이터 저장, 리소스 관리, 불필요한 작업 중단)

</aside>

SceneDelegate 메서드는 개별 화면(Scene) 단위 생명주기 이벤트를 처리

이벤트 발생 → 시스템이 SceneDelegate의 해당 메서드 호출 → 개발자가 필요한 동작 구현

### applicationDidEnterBackground와 sceneDidEnterBackground 차이

<aside>

**applicationDidEnterBackground(_:)**

**(AppDelegate)**

- 앱 전체(App-level) 차원에서 호출
- 앱이 포그라운드 → 백그라운드로 전환될 때 앱 전체 상태를 관리

**sceneDidEnterBackground(_:)**

**(SceneDelegate)**

- 각 장면(Scene-level) 차원에서 호출
- 특정 화면(Scene)이 포그라운드 → 백그라운드로 전환될 때 호출
- 즉, 화면 단위로 호출되므로, 한 앱에서 여러 Scene이 있다면 각각 호출
</aside>