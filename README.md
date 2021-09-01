# minseoksuh's WIL space

<img src="./butinhere.png" alt="butinhere image" style="width: 300px">

> In the outside world I'm a simple geologist.  
> But in HERE...I am Falcorn, defender of the Alliance.

## Web

- [Heap Snapshot](./web/heap-snapshot/index.md)
- [브라우저의 화면은 어떻게 업데이트가 되나요](./web/rendering-performance/index.md)
- [base64](./web/base64/index.md)
- [HTTPS를 이해해보자](./web/https/index.md)
- [encodeURIComponent & UTF-8](./web/encodeURIComponent/index.md)
- [svg path 이해하기](./web/svg-path/index.md)

## HTTP

- [CORS](./http/cors/index.md)
- [Cookies](./http/cookies/index.md)
- [URL의 길이와 GET의 한계](./http/url-length/index.md)
- [HTTP Cache를 사용해서 불필요한 네트워크 요청을 방지하자](./http/http-cache/index.md) (번역)

## JavaScript

- [in, hasOwnProperty](./js/in-hasownproperty/index.md)
- [closure & console.dir(obj)](./js/console.dir/index.md)
- [require vs import](./js/require-import/index.md)
- [iterator-and-generator](./js/iterator-and-generator/index.md)
- [runNonBlockingThread와 Event Loop](./js/runNonBlockingThread/index.md)
- [this 이해하기](./js/this/index.md)
- [W3 이벤트 설계 - 1](./js/event-architecture/index.md)
- [이벤트에 대해서 더 알아보자 - 2](./js/understanding-events/index.md)
- [regex 이해하기](./js/regex/index.md)
- [공룡들을 위해 설명한 현대 자바스크립트](./js/modern-javascript/index.md) (번역)

## TypeScript

- [Type Inference](./ts/type-inference/index.md)
- [Conditional Type](./ts/get-id-type/index.md)
- [Extends와 타입의 관계](./ts/extends/index.md)
- [타입가드를 통해 런타입 타입 체킹하기](./ts/type-guard/index.md)
- [Mapped types](./ts/mapped-types/index.md)
- [제네릭 타입을 사용하는 리액트 드랍다운을 만들어 보자 - 1](./ts/generic-react-component/index.md)
- [declare는 왜 사용하나요](./ts/declare/index.md)

## css

- [vertical-align, baseline](./css/verticalalign-baseline/index.md)
- [position 이해하기 - 1](./css/position/index.md) (번역/요약)
- [Stacking Context - 2](./css/stacking-context/index.md) (번역/요약)
- [Containing Block - 3](./css/containing-block/index.md) (번역/요약)
- [Normal Flow 안의 block, inline layout (+ Margin Collapsing) - 4](./css/block-inline-normal-flow/index.md) (번역/요약)

## React

- [useMemo - Dependency 내 Reference](./react/usememo-map/index.md)
- [State 로직 공유: Hooks vs render props & HOC](./react/sharing-state-logic/index.md)
- [useRef, useCallback ref](./react/useRef/index.md)
- [useState - functional updates, lazy initial State](./react/lazy-initial-state/index.md)
- [useLayoutEffect는 어떻게 동작하는가](./react/use-layout-effect/index.md)

## Package Manager

- [react-range와 Semantic Versioning](./package-manager/semantic-versioning/index.md)
- [npm scripts](./package-manager/npm-scripts/index.md)

## Web Security

- [tabnabbing vs reverse tabnabbing](./web-security/tabnabbing/index.md)

## Design Pattern

- [옵저버 패턴과 리액트](./pattern/observer/index.md)

<!-- ## Links

https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Getting_Started
https://developer.mozilla.org/en-US/docs/Web/SVG/Namespaces_Crash_Course

- [https://gist.github.com/bradtraversy/b28a0a361880141af928ada800a671d9](https://gist.github.com/bradtraversy/b28a0a361880141af928ada800a671d9)
- [https://stackoverflow.com/questions/59289801/what-is-the-difference-between-parser-options-and-environment-javascript-version](https://stackoverflow.com/questions/59289801/what-is-the-difference-between-parser-options-and-environment-javascript-version) -->

<!--

TODO: 
https://www.w3.org/TR/css-display-3/
overflow
[Critical Rendering Path](./web/critical-rendering-path/notes.md)
1. typescript version up class properties issue.

2. eslint-plugin: https://github.com/meshkorea/vroong-tms-manager-web/pull/22
- see why plugin github page does not show on SEO

3. review-count github app

4. blog

viewport and continuous media - check and report to W3C if needed

TOPICS:
how does css update? w3c

https://developer.mozilla.org/en-US/docs/Web/CSS/Visual_formatting_model

https://ui.toast.com/weekly-pick/ko_20210713

margin hoisting? https://stackoverflow.com/questions/13573653/css-margin-terror-margin-adds-space-outside-parent-element

learn more about ts union

https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes

https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flow_Layout/Flow_Layout_and_Overflow

https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flow_Layout/Intro_to_formatting_contexts

continuous media
paged media

CSS Key Concepts: CSS syntax, at-rule, comments, specificity and inheritance, the box, layout modes and visual formatting models, and margin collapsing, or the initial, computed, resolved, specified, used, and actual values. Definitions of value syntax, shorthand properties and replaced elements.
The all property resets all CSS declarations to a given known state

https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements

mdn css key concepts

- https://philipwalton.com/articles/what-no-one-told-you-about-z-index/

- https://dev.opera.com/articles/css-will-change-property/

- https://stackoverflow.com/questions/1382107/whats-a-good-way-to-extend-error-in-javascript

- eval

- https://www.youtube.com/results?search_query=authentication

- React WorkQueue

- React Scheduler: MessageChannel

- React: commitRoot, ComponentTree

- javscript while(true) project to test javscript loop

- What happens in React.createElement: ReactElement.js package: react

- React Fiber
https://www.velotio.com/engineering-blog/react-fiber-algorithm#:~:text=React%20Fiber%20is%20the%20new%20reconciliation%20algorithm%20in%20React%2016.&text=It's%20the%20old%20reconciler%20algorithm,virtualDOM%20may%20lead%20to%20confusion.

https://blog.logrocket.com/deep-dive-into-react-fiber-internals/
https://github.com/acdlite/react-fiber-architecture
https://reactjs.org/docs/codebase-overview.html
https://immigration9.github.io/react/2021/05/29/react-fiber-architecture.html

- https://babeljs.io/docs/en/babel-plugin-transform-react-jsx/

- Mime Types: https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types#javascript_types

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

- javscript modules: https://stackoverflow.com/questions/57448588/webpack-vs-es6-modules, 

- https://blog.usejournal.com/creating-a-react-app-from-scratch-f3c693b84658

- how does useState initialState gets ignored
- how does mobx work, with react? does mobx-react make the observerables a react state?

- symbol

- defer vs async

- 윤재님 깃 디렉토리 프로젝트 분석

- https://www.sitepoint.com/using-es-modules/ : es6 import deep dive

- http2

- https://github.com/facebook/react/issues/16604: hot loader

- https://www.learnenough.com/dev-environment-tutorial

- npm scripts: build:bamboo

- metaKey, ctrlKey

- https://www.learnenough.com/command-line-tutorial

- pattern: factory,

- indexedDB API?

- https://guides.github.com/features/mastering-markdown/

- 린트 룰 추가에 대해서 공부

- declarative vs imperative: https://codeburst.io/declarative-vs-imperative-programming-a8a7c93d9ad2

- functional vs oop: https://stackoverflow.com/questions/2078978/functional-programming-vs-object-oriented-programming

- AbortController

- ssh

- blob

- service workers

- vds storybook github pages

- migrate confluence articles

- github: insights - network, how does the branch lines work exactly

- SpriteSheet: https://css-tricks.com/css-sprites/

- https://developer.mozilla.org/en-US/docs/Web/CSS/backdrop-filter

- https://stackoverflow.com/questions/54438012/an-index-signature-parameter-type-cannot-be-a-union-type-consider-using-a-mappe

STUDY:
https://developer.mozilla.org/en-US/docs/Learn
https://developers.google.com/web/fundamentals
https://developers.google.com/web/fundamentals/performance/critical-rendering-path
https://developers.google.com/web/fundamentals/performance/rendering

CI / CD
git (pro git)
algorithm (CTCI)
study about web attacks
    1. session fixation
    3. csrf
    4. https://www.cisco.com/c/en_au/products/security/common-cyberattacks.html#~types-of-cyber-attacks

https://developer.mozilla.org/en-US/docs/Web/CSS: css key concepts
  (https://www.w3.org/TR/CSS2/visudet.html#containing-block-details)

https://www.w3.org/TR/CSS2/media.html#continuous-media-group

https://www.w3.org/TR/CSS2/visuren.html#normal-flow

https://stackoverflow.com/questions/12468176/what-is-a-non-replaced-inline-element & https://developer.mozilla.org/en-US/docs/Web/CSS/height

https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flow_Layout

https://www.w3.org/TR/css-flexbox-1/

-->
