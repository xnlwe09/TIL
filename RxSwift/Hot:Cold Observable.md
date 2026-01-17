# Hot/Cold Observable

생성일: 2025년 10월 21일 오후 6:50

## 개요

Observable은 항목(item)을 언제부터 방출(emit)하기 시작할까?

→ Observable에 따라 다름 !

> **Hot Observable**은 생성되자마자 항목(item)을 방출(emit) 시작할 수 있다.
> 

> **Cold Observable**은 구독할 때까지 방출(emit)을 기다리기 때문에, 처음부터 모든 Sequence를 볼 수 있다
> 

*- ReactiveX 공식문서 -*

위 내용에 따르면 Hot Observable은 Observer의 유무에 관계없이 이벤트를 방출할 수 있고,

Cold Observable은 Observer가 구독하기 전까지 대기하고, 구독하면 그때 모든 이벤트들을 방출함

<aside>

### 🔥 Hot Observable

Observer 유무에 관계없이 이벤트를 방출하는 Observable

생방송과 비슷함 → 중간에 틀면 중간부터 볼 수 있기 때문

Hot Observable의 대표적인 종류

- Publish Subject(Relay)
- Behavior Subject(Relay)
- 구독 상관없이 이벤트를 방출하고, 구독 전에 이미 방출한 이벤트는 받아볼 수 없음
</aside>

<aside>

### 🧊 Cold Observable

Cold Observable은 Observer가 구독하기 전까지 대기하다가,

구독하면 그때 모든 이벤트를 방출하는 Observable

유튜브와 비슷함 → 동영상을 틀면 항상 처음부터 나오기 때문

Cold Observable의 대표적인 종류

- Single
- just, of, from 등
- 구독 **시기**와 상관없이 처음부터 모든 데이터를 방출하고,
    
    Observable만 생성한다고 해서 방출하지 않고 구독을 해야 방출함
    
- 구독했을 때 시퀀스를 처음부터 관찰 가능. (어느 시점에서 구독을 하든지 같은 결과를 받음)
</aside>