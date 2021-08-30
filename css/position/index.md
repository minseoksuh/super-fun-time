# position 이해하기 - 1

[https://developer.mozilla.org/en-US/docs/Web/CSS/position](https://developer.mozilla.org/en-US/docs/Web/CSS/position)

[https://stackoverflow.com/questions/5011211/difference-between-static-and-relative-positioning](https://stackoverflow.com/questions/5011211/difference-between-static-and-relative-positioning)

## static

- document 정상 플로우
- top, right, bottom, left, z-index 효과 없음
- __position 기본값__

## relative

- document 정상 플로우
- 자기자신을 기준으로 top, right, bottom, left offset 적용
- offset은 주위 element들에 영향 없음 (즉 차지하는 범위는 static일때와 같음)

- z-index가 auto가 아니라면, 새로운 __stacking context를__ 만듦
- table-*-group, table-row, table-column, table-cell, table-caption elements의 영향은 정의된 바 없음

## absolute

- document 정상 플로우에서 벗어남 (layout 상 차지하는 범위 없음)
- __가장 가까운 포지션된 부모 element (static을 제외한 다른 position 값)__ 를 기준으로 위치 결정. 만약 __포지션된 부모 element__ 가 없다면, 최초 __containing block__ 을 기준으로 위치 결정.
- 최종위치는 top, right, bottom, left를 통해 결정됨

- z-index가 auto가 아니라면, 새로운 __stacking context__ 를 만듦
- absolute 포지션된 박스의 margins는 다른 margins와 collapse 하지 않음

## fixed

- document 정상 플로우에서 벗어남 (layout 상 차지하는 범위 없음)
- viewport로 정해지는 최초 __containing block__ 을 기준으로 포지션됨. 만약 부모중 하나가, `transform`, `perspective`, 또는 `filter` 프라퍼티를 `none` 말고 다른 값을 설정해준다면 그게 __containing block__ 역활을 대신함
- 최종위치는 top, right, bottom, left를 통해 결정됨

- 언제나 새로운 __stacking context__ 를 만듦
- 출력된 문서에서 fixed element는 언제나 같은 곳에 위치함

## sticky

- document 정상 플로우에 위차하다, threshold를 지나면 __nearest scrolling ancestor & containing block__ 을 기준으로 top, right, bottom, left이 적용됨
- offset은 주위 element들에 영향 없음

- 언제나 새로운 __stacking context__ 를 만듦
- 주의: sticky element들은 부모중 스크롤 메커니즘을 가지고 있는 가장 가까운 element에 붙습니다. (`overflow` 프라퍼티를 `hidden, scroll, auto, overlay` 값을 주면 스크롤 메커니즘이 생깁니다) 그 부모가 진짜 스크롤을 하고 있지 않더라도 말이죠. 이 경우 sticky 행동은 억제됩니다.

[돌아가기](../../README.md)

<!-- 
- https://developer.mozilla.org/en-US/docs/Web/CSS/Containing_block

- https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Block_formatting_context

- margin-collapsing

- https://developer.mozilla.org/en-US/docs/Web/CSS/inheritance -->
