# useRef, useCallback ref

최근에 setInterval이 돌려주는 id를 useRef로 관리할 수 있다는 얘기를 팀원을 통해 들었다.

지금까지 useRef는 리액트에서 DOM node 접근하기 위해서만 사용하는줄 알았는데, 그게 아니더라.

[https://reactjs.org/docs/hooks-reference.html#useref](https://reactjs.org/docs/hooks-reference.html#useref)

## ----이하는 위의 문서에 대한 번역입니다.----

useRef는 수정가능한 ref 오브젝트를 돌려주고, current 프라퍼티는 인자로 넘겨진 값으로 설정됩니다.
**ref 오브젝트는 컴포넌트의 전체 수명동안 살아있습니다**

> A common use case is to access a child imperatively
> (리액트는 기본적으로 declarative 해서 개발자가 무엇을 보여줄지 컴포넌트로 표현하고 DOM을 manipulate 하는 것은 under the hood 로 처리 되는데, useRef를 통해 직접 접근하기 때문에 imperatively 란 단어를 사용한것 같다.)

```jsx
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    // `current` points to the mounted text input element
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

쉽게 말해서, useRef는 변경 가능한 값을 current에 들고 있을 수 있는 "상자" 같은 것입니다.

ref 오브젝트를 `jsx <div ref={myRef} />` 이렇게 넘겨주면, 리액트는 해당 노드가 바뀔때 current를 해당 DOM node로 설정해줍니다.

**그러나 useRef()는 jsx ref attribute을 제외하고도 유용하게 사용할 수 있습니다. 클래스의 인스턴스 필드와 같이 변화 가능한 어떤 값들도 저장할 수 있습니다.**

이게 가능한 이유는 useRef()는 일반 자바스크립트 오브젝트를 만들기 때문입니다. useRef를 사용하는것과 당신이 직접 {current: ...} 오브젝트를 만드는 것의 유일한 차이점은 useRef는 모든 render에 같은 ref 오브젝트를 돌려준다는 점.

**유의해야 할 점은 useRef는 내용물이 바뀔때 알려주지 않는다는 점입니다. current 프라퍼티를 바꾸는 것은 rerender를 일으키지 않습니다. 만약 당신이 ref를 DOM node에 붙이거나 땔때 어떤 코드를 실행하고 싶다면, "callback ref"를 사용해보세요.**

```jsx
function MeasureExample() {
  const [height, setHeight] = useState(0);

  const measuredRef = useCallback((node) => {
    if (node !== null) {
      setHeight(node.getBoundingClientRect().height);
    }
  }, []);

  return (
    <>
      <h1 ref={measuredRef}>Hello, world</h1>
      <h2>The above header is {Math.round(height)}px tall</h2>
    </>
  );
}
```

---

위와 같이 useCallback을 ref로 넘겨주면, 해당 DOM node가 변경될때마다 콜백 코드가 실행이 됩니다. 적절한 상황에 사용하면 유용할듯.

[돌아가기](../../README.md)
