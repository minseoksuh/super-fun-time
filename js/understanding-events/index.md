# 이벤트에 대해서 더 알아보자 - 2

저번 이벤트 설계 관련 글은 너무 개념적이어서 좀더 실용적으로 이벤트를 이해해보고자 여러 도움이 되는 정보를 정리해보았습니다.

> Another thing worth mentioning at this point is that events are not unique to JavaScript — most programming languages have some kind of event model, and the way the model works often differs from JavaScript's way.

- 여러 형태의 이벤트 모델이 있고 자바스크립트 모델과 다른점이 많다. (ex: node.js 이벤트 모델)

> Web events are not part of the core JavaScript language — they are defined as part of the APIs built into the browser.

- 이벤트는 자바스크립트 언어에 포함되지 않음 - 브라우저 api의 한 부분으로 정의 되어 있음.

- 이벤트가 발생할때마다 실행되는 코드를 event handler 또는 event listener 이라고 합니다. 이벤트 핸들러를 이벤트에 등록해서 사용합니다. (registering an event handler)

## 이벤트 핸들러 등록 방법

1. 엘레멘트의 property를 통해 핸들러 추가 (onclick, onplay, onfocus, ...etc)

   ```js
   const btn = document.querySelector("button");

   btn.onclick = function () {
     const rndCol =
       "rgb(" + random(255) + "," + random(255) + "," + random(255) + ")";
     document.body.style.backgroundColor = rndCol;
   };
   ```

2. 인라인으로 핸들러 추가 (BAD PRACTICE: 코드가 더러워짐, 관심사 분리가 안됨)

   ```html
   <button onclick="bgChange()">Press me</button>
   ```

3. addEventListener, removeEventListener

   ```js
   const controller = new AbortController();
   btn.addEventListener(
     "click",
     function () {
       var rndCol =
         "rgb(" + random(255) + "," + random(255) + "," + random(255) + ")";
       document.body.style.backgroundColor = rndCol;
     },
     { signal: controller.signal }
   ); // pass an AbortSignal to this handler

   // AbortController를 사용해서 이벤트 핸들러를 제거할수 있다고 합니다.
   // (removeEventListener 말고 다른 방법)

   // 이 방법의 가장 큰 이점은 1번 방법과 달리 핸들러로 여러 함수를 등록할 수 있다는 점

   // addEventListener 내부의 this는 자동적으로 핸들러를 추가한 엘레멘트가 됩니다.
   ```

!: 1번은 더 기본적인 방법으로 브라우저 지원이 더 잘되고, 3번은 여러 핸들러를 관리 할수 있어서 둘 중에 잘 판단해서 사용하라고 합니다.

## 이벤트 Capturing과 Bubbling

이벤트 관련해서 제가 가장 모르는 부분이었던 것 같습니다.

저번 "이벤트 설계" 글에서 말했듯이 이벤트가 발생하면 DOM 에서 event object를 타겟 엘레멘트로 부모 엘레멘트들을 거쳐서 보내고(capturing) 타겟에서 이벤트 처리 후 event object는 다시 부모 엘레멘트를 거쳐서 DOM 에 돌아갑니다(bubbling).

- 핵심은 이 과정에서 타겟에 달린 이벤트 핸들러 뿐만 아니라 부모 엘레멘트들의 이벤트 핸들러들도 같이 실행된다는 점입니다. (그래서 stopPropagation을 써서 원치 않는 이벤트 핸들러가 동작하는걸 저희가 막죠)

- 예전에 웹 초창기때 Microsoft와 Netscape가 이벤트 모델을 분기 되게 만들었는데, Microsoft는 capturing 과정에서 부모들의 핸들러를 실행시켰다면, Netscape는 bubbling 과정에서 핸들러를 실행시켰다고 합니다. W3에서 스펙을 재정의할 때에는 두 방식을 모두 수용할 수 있도록 바뀌었습니다 (부모 이벤트 핸들러들이 capturing 에서도 실행 가능하고 bubbling에서도 실행 가능함).

- **_Modern 브라우저들은 default로 bubbling phase 에서 부모의 핸들러들을 실행시킵니다._**

- `addEventListener(_, __, true)` 를 사용하면 (3번째 인자가 true, default는 false) capturing phase 에 부모의 이벤트 핸들러를 추가할 수 있습니다. 이때 주의해야 할점은 해당 이벤트를 remove 하려면 removeEventListener도 같은 타이밍 옵션으로 실행시켜줘야 한다는 것. `removeEventListener(_, __, true)`

- stopPropagation을 하면 그 이후에 거치는 이벤트 핸들러가 발동하지 않습니다. 즉 target element에서 stopPropagation을 해도 capturing phase에 달려 있는 이벤트 핸들러들은 이미 실행이 되었기 때문에 취소 되지 않습니다.

- 거의 모든 이벤트는 버블링이 됩니다 (focus 같은 경우는 버블링 되지 않음)

- **_GA 같이 event 발생여부를 DOM 레벨에서 체크하는 로직 때문에 필요하지 않다면 stopPropagation을 하지 않는게 좋다고 합니다._**

> If an element has multiple event handlers on a single event, then even if one of them stops the bubbling, the other ones still execute.
> In other words, event.stopPropagation() stops the move upwards, but on the current element all other handlers will run.
> To stop the bubbling and prevent handlers on the current element from running, there’s a method event.stopImmediatePropagation(). After it no other handlers execute.

- stopImmediatePropagation은 해당 엘레멘트에 붙어있는 다른 이벤트까지 막습니다.

- preventDefault()를 사용해서 기본 이벤트 반응 스킵 가능

## currentTarget vs Target

- Target: 최초 이벤트 발생지점 (ex: 누른 버튼)
- currentTarget: event 오브젝트가 핸들러를 통해 접근 가능할 때 현재 지나가고 있는 엘레멘트 (ex: 캡쳐, 버블링 페이즈 때 지나치는 부모 엘레멘트 또는 target 엘레멘트)

## 참고

- [https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)

- [https://www.quirksmode.org/js/introevents.html](https://www.quirksmode.org/js/introevents.html)

- [https://www.quirksmode.org/js/events_order.html](https://www.quirksmode.org/js/events_order.html)

- [https://javascript.info/bubbling-and-capturing](https://javascript.info/bubbling-and-capturing)

[돌아가기](../../README.md)
