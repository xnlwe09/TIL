# tableView

생성일: 2025년 8월 20일 오후 10:26

## UITableView란?

**하나의 열에 서로로 스크롤되는 콘텐츠 행들을 표시하는 것**

→ 스크롤을 할 수 있기 때문에 UIScrollView를 상속받고 있음 (따로 상속 안 받아두 댐)

## cell

UITableView는 각 행의 콘텐츠를 표시하는 cell로 구성

표준 cell 구성은 텍스트 + 이미지의 단순한 조합이지만 사용자 커스텀 cell을 만들 수도 있음

또 header, footer를 생성해 각 그룹에 대한 추가적인 정보를 제공할 수 있음

## UITableViewCell

테이블뷰(UITableView)의 각 행(row)을 나타내는 뷰(View)
→ 테이블의 한 줄 한 줄을 UI 단위로 표현하는 객체

해당 View를 통해 각 행이 어떻게 보여질지 결정

**기능**

1. 내용 표시
    - 텍스트(textLabel)
    - 서브텍스트(detailTextLabel)
    - 이미지(imageView)
2. 선택 상태 관리
    - 셀을 선택/해제했을 때 색상 하이라이트, 액션 처리
3. 커스터마이징 기능
    - 기본 제공 레이블/이미지 외에도 UITableViewCell을 상속받아 Custom cell을 구성해서
        
        원하는 UI 구성, 레이아웃, 동작까지 자유롭게 설정 가능
        

### delegate 메서드랑 datasource 메서드를 작성해야한다네요,,

```swift
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    // 1. 재사용 셀 가져오기
    let cell = tableView.dequeueReusableCell(withIdentifier: "identifier", for: indexPath)
    
    // 2. 셀 설정하기 (텍스트, 이미지, 색상 등)
    // cell.textLabel?.text = "내용"
    
    // 3. 완성된 셀 반환하기
    return cell
}
```