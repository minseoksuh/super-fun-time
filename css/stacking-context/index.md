# Stacking Context - 2

[https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)

![understanding_zindex_04.png](./understanding_zindex_04.png)

위에 그림을 보면 모든 element들이 자신의 stacking context를 만들어낸다. (position, z-index 때문)  
stacking context 계층을 보면 다음과 같다.

- Root
  - DIV #1
  - DIV #2
  - DIV #3
    - DIV #4
    - DIV #5
    - DIV #6

> It is important to note that DIV #4, DIV #5 and DIV #6 are children of DIV #3, so stacking of those elements is completely resolved within DIV#3. Once stacking and rendering within DIV #3 is completed, the whole DIV #3 element is passed for stacking in the root element with respect to its sibling's DIV.

DIV #4, DIV #5, DIV #6은  DIV #3의 자식이기 때문에 4, 5, 6의 stacking은 DIV #3 안에서 해결이 된다. (resolved) DIV #3 내에서 stacking과 rendering이 완료되면, DIV #3이 전체로서 root element에 형제 div들과 위치된다.

> 노트:  
>
> - div4의 z-index가 `6`이고 div1의 z-index가 `5`인데도, div4가 div1 밑에 위치되는 이유는 4의 `z-index: 6`은 부모인 div3의 stacking context 안에서만 효력이 있기 때문. div3의 z-index가 `4`이기 때문에, div3 내의 자식들이 어떤 z-index를 가지고 있어도 div1보다 밑에 위치된다.
> - 같은 이유로 div2는 div5 보다 밑에 위치된다. (div5는 div3의 자식이고, div3의 z-index `4`가 div2의 z-index `2`보다 높기 때문에)
> - div3의 z-index는 `4` 이지만 div4, div5, div6의 z-index와는 별개이다. (div3은 root의 stacking context에 속하기 때문)
> - __스태킹 순서를 파악하기 쉬운 방법은 stacking을 일종의 "version number"로 생각하는것. 자식이 z-index가 minor version 이라고 생각하고, 부모의 z-index가 major version 이라고 생각해보면 좀 더 명확하게 파악이 된다.__
>
> - Root
>   - div2: 2.0
>   - div3: 4.0
>     - div5: 4.1
>     - div6: 4.3
>     - div4: 4.6
>   - div1: 5.0


## 개념 요약

- stacking context는 다른 context 안에 포함될수 있고, 계층이 생성된다.
- 각 stacking context는 형제 element들과는 완전히 별개이다: stacking 프로세스 중 자식 element 만 고려된다.
- 각 stacking context는 __self contained__ 이다. 안의 자식 element들의 stacking이 끝나면, 부모 element가 하나의 context로 부모 stacking context 안에 위치한다.

## Stacking Context 생성 시점

- Root element of the document (`<html>`).
- Element with a position value absolute or relative and z-index value other than auto.
- Element with a position value fixed or sticky (sticky for all mobile browsers, but not older desktop).
- Element that is a child of a flex container, with z-index value other than auto.
- Element that is a child of a grid container, with z-index value other than auto.
- Element with a opacity value less than 1 (See the specification for opacity).
- Element with a mix-blend-mode value other than normal.
- Element with any of the following properties with value other than none:
  - transform
  - filter
  - perspective
  - clip-path
  - mask / mask-image / mask-border
- Element with a isolation value isolate.
- Element with a -webkit-overflow-scrolling value touch.
- Element with a will-change value specifying any property that would create a stacking context on non-initial value (see this post).
- Element with a contain value of layout, or paint, or a composite value that includes either of them (i.e. contain: strict, contain: content).

[돌아가기](/README.md)
