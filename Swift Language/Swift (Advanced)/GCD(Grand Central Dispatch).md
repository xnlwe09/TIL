# GCD(Grand Central Dispatch)

## GCD(Grand Central Dispatch)란?

동시성 프로그래밍을 쉽게 구현하고 관리할 수 있도록 Apple이 제공하는 프레임워크(API)로,
개발자가 Thread를 직접 생성하거나 관리하지 않고 Queue에 Task를 전달하면
시스템이 Queue의 실행 방식에 따라 적절한 Thread를 관리하고 Task 실행을 조절함

즉, 개발자가 선택한 Queue에 작업(Task)을 보내면
GCD가 Queue의 특성에 맞게 Thread를 관리하고
Task 실행을 조절하는 방식으로 동시성 프로그래밍을 구현할 수 있음

<aside>

## 📍개념 용어 정리

- Queue(큐) : 실행할 Task를 저장하고 관리하는 공간
큐의 종류에 따라 Task 실행 방식(순차 실행/동시 실행)이 결정됨
(개발자가 적절한 Queue를 선택해 Task를 전달하면,
GCD가 해당 Queue의 특성에 맞게 Thread 관리와 실행을 조절)
- Task(작업) : 큐에 넣는 코드 블록(클로저)
- Thread(스레드) : 실제 코드가 실행되는 단위
- Dispatch : 작업을 큐에 보내는 것

**쉽게 말해서 !**

Task : 할 일 (작업)

Thread : 일 처리하는 노동자

Queue : 노동자의 할 일 리스트

</aside>

메인 스레드가 UI 그리기랑 사용자 입력 처리만 담당해야하는데 모든 Task가 메인 스레드로 가면 앱이 프리징날 수 있어서 그 Task들은 개발자가 작업 목적에 맞는 큐에 전달해줘야함

#### → 개발자가 Task를 Queue에 전달하면, GCD가 Queue에 맞는 Thread에서 실행되도록 관리

- UI 작업 → 메인 큐에 보냄
- 무거운 작업 → 백그라운드 큐에 보냄

<aside>

### 📎 메인 큐(Main Queue)
: Main Thread에서 실행될 Task를 처리하는 큐

- UI 업데이트 등 Main Thread에서 실행되어야 하는 Task 처리
- Serial Queue → 순서대로 하나씩 실행
    - 한 작업이 끝나야 다음 작업이 실행됨
</aside>

<aside>

### 📎 글로벌 큐(Global Queue)
: Background Thread에서 실행될 Task를 처리하는 큐

- 무거운 Task나 동시 처리 작업을 처리함
- Concurrent Queue → 여러 작업 동시 실행 가능
    - 시스템이 필요한 만큼 스레드를 관리하여 Task를 처리 (순서 보장은 안됨)
</aside>

<aside>

### 커스텀 큐(Custom Queue) : 개발자가 직접 만들고 속성을 지정할 수 있는 큐

- 특정 작업을 원하는 방식으로 처리하고 싶을 때 사용
- 특정 목적이나 로직에 맞춰 작업 처리 순서와 동시성 제어 가능
- Serial(직렬), Concurrent(동시) 둘 다 가능해서 선택해서 사용하면 됨
</aside>

## 실행 방식

async : 비동기 실행 → 큐에 넣고 바로 리턴 (작업 완료를 기다리지 않음)

sync : 동기 실행 → Task가 완료될 때까지 현재 Thread가 대기
(main 스레드에서 메인 큐에 sync를 호출하면 Deadlock이 발생할 수 있음)

## GCD 장점

1. UI 프리징 방지 → 메인 스레드에서 무거운 작업을 피할 수 있음
2. 동시성 처리 → 여러 Task를 Queue에서 관리하고, 적절한 Thread에서 실행하여 효율적으로 처리 가능