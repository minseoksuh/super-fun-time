# 이벤트 구조

[https://www.w3.org/TR/DOM-Level-3-Events/#dom-event-architecture](https://www.w3.org/TR/DOM-Level-3-Events/#dom-event-architecture)

![event-flow](./eventflow.svg)

개발을 하던 와중 이벤트 관련 버그가 있어서

preventDefault, stopPropagation, stopImmediatePropagation을 남발하던 와중

자신에 대한 회의감을 느껴서 한번 공부를 해보기로 했다.

w3 스펙 내용중 핵심적이라고 생각되는 것만 추려서 정리해보겠습니다.

## DOM Event Architecture

This section is non-normative. Refer to [DOM](https://dom.spec.whatwg.org/) for a normative description of the DOM event architecture

### 3.1 Event Displatch and Dom event flow

이벤트가 dispatch 되기 전에 우선 propagation path가 정해진다고 합니다. 이 path 는 event target에 도달하기 위한 node들의 목록으로,
이 목록 마지막에 있는게 event target이라고 합니다.

path 가 정해지면 본격적으로 이벤트 오브젝트가 움직이는데 event dispatch가 시작되는데 여기에 3 phase 가 있습니다.

    1. Capture phase: Window 에서 발생한 이벤트 오브젝트가 조상 엘레멘트들을 타고타고 가서 event target의 부모 노드를 찾아내는 과정
    2. Target phase: 이벤트 오브젝트가 목적지에 도달한 과정
    3. Bubble phase: 이벤트 오브젝트가 다시 Window로 되돌아가는 과정 (연어가 강물을 거슬러 올라가..)

    - 이벤트 오브젝트의 bubbles 필드가 false라면 Bubble phase가 스킵됩니다.
    - dispatch 전에 stopPropagation이 불린다면 모든 phase가 스킵됩니다.

### 3.2 Default actions and cancelable events

이벤트 중에 default action이 있고 이 action들이 취소가 가능한 이벤트를 cancelable 이벤트라고 한다고 합니다.

이런 cancelable 한 이벤트를 preventDefault() 하면 default action 이 실행이 안되거나, 실행 된후 효과가 롤백되거나 한다고 합니다.

> ex1) mousedown 이벤트의 default action 중 하나는 마우스가 텍스트 위에 있으면 "텍스트 선택" 이미지 위애 있으면 "이미지 드래그". 여기서 preventDefault를 하면 해당 현상이 발현 안된다고 합니다.
> ex2) 체크 박스를 클릭하면 기본적으로 "checked IDL attribute value" 를 토글한다고 합니다. 이 경우 prventDefault가 되면 해당 현상이 벌어지고 그 이후에 로백된다고 합니다.

- defaultPrvented attribute을 통해 이벤트가 취소됬는지 확인 가능
- dispatchEvent()로 해서 만들어진 이벤트의 return 값을 통해 이벤트가 취소됐는지 확인 가능 (false: 취소됨.)

### 3.3 동기 이벤트 비동기 이벤트

이벤트중에 virtual queue에 FIFO 모델로 들어가는 synchronous 한 이벤트가 있고 그 흐름에서 벗어나는 asynchronous 이벤트가 있다고 합니다.

### 3.4 Trusted 이벤트

user agent: A program, such as a browser or content authoring tool, normally running on a client machine, which acts on a user’s behalf in retrieving, interpreting, executing, presenting, or creating content. Users MAY act on the content using different user agents at different times, for different purposes.

#### isTrusted: true

user agent 에 의해서 생성된 이벤트 또는 DOM의 변화를 통해 직접적으로 생성된 이벤트들은 isTrusted: true 라고 합니다. (createEvent로 만들어진 )

#### isTrusted: false

- createEvent 를 통해 만들어진 이벤트
- initEvent 를 통해 수정된 이벤트
- dispatchEvent를 통해 dispatch 된 이벤트

> 신뢰 없는 이벤트들은 (untrusted events)는 default actions 가 동작하지 않습니다. (클릭 이벤트는 예외) 마치 prventDefault가 미리 불린것처럼 동작

### 3.5 Activation triggers and Behavior

어떤 event target 들은 activation behavior 가 있고 그 행동을 발현시키기 위한 activation trigger 가 있다고 합니다.

> ex) <a></a> 태그 activation trigger
> activation behavior: 그 링크 주소로 이동하는것
> activation trigger: 링크 클릭, 링크에 focus 가 있는 상태에서 "Enter" 키 누르기

#### 3.6 마우스, 키보드 이벤트 만들기

> However the KeyboardEvent and MouseEvent interfaces provide additional dictionary members for initializing the internal state of the Event object’s key modifiers: specifically, the internal state queried for using the getModifierState() and getModifierState() methods.
> For the purposes of constructing a KeyboardEvent, MouseEvent, or object derived from these objects using the algorithm below, all KeyboardEvent, MouseEvent, and derived objects have internal key modifier state which can be set and retrieved using the key modifier names described in the Modifier Keys table in [UIEvents-Key].

이건 나중에 필요할거 같으면 분석하겠습니다.

[돌아가기](/README.md)
