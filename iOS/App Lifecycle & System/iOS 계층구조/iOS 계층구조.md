# iOS 계층구조

## iOS 계층구조란?

**iOS가 운영체제 기능을 여러 단계로 나누어**

**개발자와 사용자가 더 쉽게 사용할 수 있도록 정리한 구조**

iOS는 아래층부터 Core Os, Core Service, Media, Cocoa Touch로 이루어져있으며

아래 계층으로 갈수록 가장 기본이 되는 계층이고

위 계층으로 갈 수록 사용자 관련 계층이다.

(하위 계층은 iOS의 핵심 부분/하드웨어에 가까움)

![image.png](iOS%20%EA%B3%84%EC%B8%B5%EA%B5%AC%EC%A1%B0/image.png)

<aside>

### 📍Cocoa Touch

화면의 그래픽 UI 터치의 기능 제공

UIKit(UI 구성, 터치), MapKit(지도), MessageUI(메세지, 이메일) 같은 UI 프레임워크가 있음

- 사용자 인터페이스(UI) 구성 기능
- 멀티터치 이벤트 처리 등의 기능
</aside>

<aside>

### 📍Media

그래픽이나 오디오, 비디오 등 멀티미디어 기능 제공

AVFoundation(오디오 / 비디오 재생 및 녹음), Core Animation(애니메이션 처리) 등의 프레임워크

</aside>

<aside>

### 📍Core Service

앱 로직과 데이터 처리의 기반 계층

Core OS에서 제공하지 않는 기능들을 포함

내부 데이터 / 위치 / 센서 등의 기능 제공

Foundation(데이터 관리), CloudKit(iCloud 연동), Core Location(위치 기반 서비스) 등의 프레임워크

</aside>

<aside>

### 📍Core OS

하드웨어와 가장 가까이 있는 최하위 계층

시스템의 핵심 기능을 포함하는 기본적인 부분들을 관리

하드웨어와 직접 연결된 최소 단위 기능을 담당하고, 그 위에서 Core Service 같은 상위 계층이

이 기능들을 더 쓰기 편리하게 감싸서 제공

- Darwin
- Security
- Power Management
- File System Access
- Low-level Networking
</aside>