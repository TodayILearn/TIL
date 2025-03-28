# 문제점

- 요소의 `크기 오차`가 발생함 (content-box 사용)

> `box-sizing`의 기본값인 `content-box`를 사용할 때, 요소의 실제 크기는 설정한 너비와 높이에 패딩과 테두리가 추가되기 때문에 레이아웃이 예상치 못하게 깨지는 경우 발생함.<br>
> 예를 들어, `width: 100px; padding: 10px; border: 5px solid black;`로 설정된 요소의 실제 너비는 `130px`가 되어, 레이아웃이 의도한 대로 정렬되지 않는 문제가 발생함.

- 그리드 및 플렉스박스와의 관계

> CSS greed나 flex-box를 사용할 때, `box-sizing` 속성이 요소의 크기 계산에 영향을 미쳐, 레이아웃이 복잡해지는 경우가 있었습니다.

# 해결법

1. `border-box` 사용

   - `box-sizing: border-box;`를 사용하여 요소의 너비와 높이를 콘텐츠 영역, 패딩, 테두리를 모두 포함하여 계산하도록 설정함.
   - 예를 들어, `width: 100px; padding: 10px; border: 5px solid black;`로 설정된 요소의 실제 너비는 `100px`가 되어, 레이아웃이 의도한 대로 정렬됨.

2. 전역 설정
   - 모든 요소에 `box-sizing: border-box;`를 적용하여 일관된 레이아웃을 유지하도록 했습니다.

# 느낀점

- border-box를 사용하면 요소의 크기를 더 `직관적`으로 관리할 수 있어, 레이아웃이 더 `예측 가능`하고 `유지보수`가 쉬워짐.
- CSS 전역설정을 border-box 기본 설정으로 하는것도 좋아보임.
- CSS에서 요소 크기에 오차가 생길 경우 박스사이징 관련 문제가 아닐지 의심해야함.
