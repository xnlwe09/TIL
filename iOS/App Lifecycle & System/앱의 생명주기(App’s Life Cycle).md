# 앱의 생명주기(App’s Life Cycle)

생성일: 2025년 8월 20일 오후 10:26

## 앱의 생명주기(App’s Life Cycle)

**App의 실행/종료 및 App이 Foreground/Background 상태에 있을 때,
시스템이 발생시키는 event에 의해 App의 상태가 전환되는 일련의 과정**

App은 여러가지 App이 한 번에 실행될 수도 있고, 어떤 앱을 사용하다가 또 다른 앱을 사용할 수도 있음

그럼 앱이 다른 앱으로 전환되거나 백그라운드로 전환될 수도, 앱이 종료될 수도 있음

이런 시점에 운영체제가 자동으로 호출하는 메서드가 존재하며, 이런 메서드 실행의 과정

## Foreground

App의 실행화면(Scene)을 사용자에게 보여주는 상태(영역)

## Background

App의 실행화면(Scene)이 내려간 상태(영역)

## 앱의 상태(App State)

<aside>

### Not Running

App이 실행 중이지 않거나 종료된 상태

</aside>

<aside>

### **Foreground - Active**

App이 실행 중이고 사용자 이벤트를 받아서 상호작용할 수 있는 상태

(바로 Active상태는 될 수 없으며 Inactive 상태를 거쳐서 Active 상태가 됨)

</aside>

<aside>

### Foreground - Inactive

App이 실행 중이지만 사용자로부터 이벤트를 받을 수 없는 상태

(앱 실행 중 전화, 알림 같은 이벤트 등에 의해 앱을 사용할 수 없게 되는 경우)

</aside>

<aside>

### Background - Running

홈 화면으로 나가거나 다른 앱으로 전환되어 앱의 화면은 내려갔지만 계속 작동하는 상태

Apple은 보안 등의 이유로 Background 영역에서 App의 작동을 허용하지 않지만 일부 App은 작동 가능 → 음악 앱을 닫아도 재생한 음악이 계속 실행되는 경우, 타이머가 계속 실행되는 등의 작업

</aside>

<aside>

### Suspended

App이 Background 상태에 있으면서 앱을 다시 실행했을 땐

최근 작업을 빠르게 로드하기 위해서 메모리 관련 데이터만 저장해둔 상태

CPU 자원은 거의 사용하지 않고(걍 앱이 멈춘 상태) 메모리에서도 실행되지 않음

→ 앱이 Background 상태에 진입했을 때 다른 작업을 하지 않으면 Suspended 상태로 진입

Suspended 상태의 앱들은 메모리가 부족해지면 시스템에 의해 강제 종료될 수 있음

</aside>
