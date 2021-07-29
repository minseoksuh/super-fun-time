# position

[https://developer.mozilla.org/en-US/docs/Web/CSS/position](https://developer.mozilla.org/en-US/docs/Web/CSS/position)

[https://stackoverflow.com/questions/5011211/difference-between-static-and-relative-positioning](https://stackoverflow.com/questions/5011211/difference-between-static-and-relative-positioning)

## static

- document 정상 플로우에 의해 위치 결졍
- top, right, bottom, left, z-index 효과 없음
- __position 기본값__

## relative

- document 정상 플로우에 의해 위치 결정
- 자기자신을 기준으로 top, right, bottom, left offset 적용
- offset은 주위 element들에 영향 없음 (즉 차지하는 범위는 static일때와 같음)
- z-index가 auto가 아니라면, 새로운 stacking context를 만듦

## absolute

- document 정상 플로우에서 벗어남 (layout 상 차지하는 범위 없음)
- It is positioned relative to its closest positioned ancestor, if any; otherwise, it is placed relative to the initial __containing block__
- 최종위치는 top, right, bottom, left를 통해 결정됨
- z-index가 auto가 아니라면, 새로운 __stacking context__ 를 만듦
- The margins of absolutely positioned boxes do not collapse with other margins.

## fixed

- document 정상 플로우에서 벗어남 (layout 상 차지하는 범위 없음)
- viewport로 정해지는 최초 containing block을 기준으로 포지션됨. 만약 부모중 하나가, `transform`, `perspective`, 또는 `filter` 프라퍼티를 `none` 말고 값을 설정해준다면 그게 containing block 역활을 대신함
- 최종위치는 top, right, bottom, left를 통해 결정됨
- 언제나 새로운 __stacking context__ 를 만듦

## sticky

- document 정상 플로우에 의해 위치 결정
- 그러다가 threshold를 지나면 "가장 가까운 스크롤 부모 & containing block" 을 기준으로 offset이 들어감
- offset은 주위 element들에 영향 없음
- 언제나 새로운 __stacking context__ 를 만듦
- 주의: 스티키 element들은 부모중 스크롤 메커니즘을 가지고 있는 가장 가까운 element에 붙습니다. (overflow: hidden, scroll, auto, overlay) 이 행동은 그 부모가 진짜 스크롤을 하고 있는지와는 별개로 동작함.

[돌아가기](./README.md)

<!-- 
- https://developer.mozilla.org/en-US/docs/Web/CSS/Containing_block

- https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context

- https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Block_formatting_context

- margin-collapsing

- https://developer.mozilla.org/en-US/docs/Web/CSS/inheritance -->
