# Type Inference

[https://www.typescriptlang.org/docs/handbook/type-inference.html](https://www.typescriptlang.org/docs/handbook/type-inference.html)

타입 스크립트 타입 추론 기능이 작동하는 법에 대해 조사를 해보아요

> This kind of inference takes place when initializing variables and members, setting parameter default values, and determining function return types.

아래 상황에서 작동한다고 해요

- 변수 또는 멤버 초기화 시 (변수, 멤버 값 추론)
- 파라메터 최초값 세팅시 (파라메터 값 추론)
- 함수 리턴 시 (리턴 값 추론)

## Best Common Type

여러 혼합 타입에 대하여 타입스크립트가 타입을 추론하는 방법

```ts
let x = [0, 1, null];
//  ^ = let x: (number | null)[]
let zoo = [new Rhino(), new Elephant(), new Sanke()];
//    ^ = let zoo: (Rhino | Elephant | Snake)[]
```

## Contextual Typing

어떤 표현에 대한 타입이 그 표현의 위치에 의해 결정되는 상황.

```ts
window.onmousedown = function (mouseEvent) {
  console.log(mouseEvent.button); // OK
  console.log(mouseEvent.kangaroo); // Error!
};

window.onscroll = function (uiEvent) {
  console.log(mouseEvent.button); // Error!
};
```

[돌아가기](../../README.md)
