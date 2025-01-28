# 마진 병합이란?

- 두 개의 인접한 요소의 마진(margin)이 하나로 합쳐지는 현상입니다.

## 마진 병합이 일어나는 경우

1. 인접한 형제요소 사이 상하 마진이 겹치는 경우
2. 부모 요소와 자식요소 사이 상하 마진이 겹치는 경우

   - 부모와 자손을 분리하는 요소가 없음
   - 부모 블록에 padding, border, inline content가 없음
   - 부모의 부모의 margin-bottom과 자손의 margin-bottom을 분리할 height, min-height, max-height가 존재하지 않음음

3. 빈 요소의 상하 마진이 겹치는 경우
   - padding, border, inline content, height, min-height, max-height가 없으면 블록의 margin-top과 margin-bottom이 더 큰 값으로 상쇄된다.

## 마진 병합 예외

- 플로팅 요소와 요소에 절대 위치(position: absolute)를 지정한 경우
- 박스가 display: flex이거나 grid 인 경우
- 수평 마진일 경우

## 해결법

1. 겹치는 마진 사이에 공간을 차지하는 요소들을 삽입 해준다.

   - table태그를 넣어준다.
   - border값을 적용해준다.
   - padding을 넣어준다.
   - 글자를 삽입한다.

2. display: inline-block;을 적용해 준다.

   - 마진 병합현상은 block 요소에만 적용되기 때문이다.

3. 부모 요소에 overflow: hidden;을 적용해준다.

   - overflow:hidden을 사용하면 새롭게 block format context가 만들어지면서 병합되었던 마진 값을 출력해 준다. overflow를 사용한 요소는 내부에 마진을 포함하는 새로운 독립적인 요소가 되기 때문에 마진 병합을 해결할 수 있다.

4. margin 대신 padding으로 간격을 조정한다.

### 느낀점

```

1번의 경우 의도한 디자인에 벗어난 디자인이 되는 경우가 있고,
2번은 자식 요소에 존재하는 모든 마진 병합 현상이 사라지게 되고,
4번은 padding의 경우 박스 크기가 커지게 만들고 디자인 통일성을 깨는 경우가 나올 수 있다고 생각하여,
3번을 사용하여 현상을 해결하는게 바람직하다고 생각한다.

```
