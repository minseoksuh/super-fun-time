# State 로직 공유: 커스텀 Hook, render props, HOC

[https://reactjs.org/docs/hooks-custom.html](https://reactjs.org/docs/hooks-custom.html)

커스텀 Hook이 뭔지 리액트 Doc을 찾아봤더니

그냥 제공되는 Hooks를 함수로 감싸서 자주 사용되는 로직을 모듈화 시키는 것이었다.

[custom-hook.png](./customHook.png)

> 내부에서 state를 사용하지는 않지만 현재 메쉬코리아 프로젝트에 사용되는 useDidMount 도 일종의 custom Hook 이라고 할 수 있을듯.
>
> ```tsx
> const useDidMount = (fn: () => void) => useEffect(fn, []);
> ```

글을 읽다가

> Traditionally in React, we’ve had two popular ways to share stateful logic between components: render props and higher-order components. We will now look at how Hooks solve many of the same problems without forcing you to add more components to the tree.
