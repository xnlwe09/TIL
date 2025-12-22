# CG@@

생성일: 2025년 8월 20일 오후 10:26

## 개요

**CoreGraphics 프레임워크에서 제공하는 구조체**

## CGPoint

**2차원 좌표계의 점을 포함하는 구조체**

→ 정의만 보면 어려우니까 쉽게 말해서 iOS에서 x, y 좌표를 나타내주는 것

주로 뷰의 위치, 터치한 좌표 같은 걸 표현할 때 사용

```swift
public struct CGPoint {
	public var x: CGFloat
	public var y: CGFloat
	public init()
	public init(x: CGFloat, y: CGFloat)
}
```

x 좌표와 y 좌표를 가지는 구조체임!

## CGSize

**너비와 높이 값을 포함하는 구조체**

(사각형 아님. 실제 사각형 절대 아님)

주로 뷰의 폭과 높이, 이미지 크기 등을 표현할 때 사용

```swift
public struct CGSize {
	public var width: CGFloat
	public var height: CGFloat
	public init()
	public init(width: CGFloat, height: CGFloat)
}
```

너비랑 높이만을 가지고 있음

## CGRect

**사각형의 위치와 크기를 포함하는 구조체**

CGRect는 CGSize와 다르게 사각형

→ CGRect는 너비랑 높이 말고도 원점(origin)을 가지고 이씀

```swift
public struct CGRect {
	public var origin: CGPoint
	public var size: CGSize
	public init()
	public init(origin: CGPoint, size: CGSize)
}
```


CGRect는 사각형인데 iOS에서는 사각형을 그리려면 위치를 알아야 함!

**CGRect : 사각형의 위치와 크기를 포함하는 구조체**

→ 위치가 origin, 크기가 size

그 위치를 CGPoint로 나타내고, 크기(너비와 높이)를 너비, 높이를 구조체 변수로 가지는 CGSize로 정함


