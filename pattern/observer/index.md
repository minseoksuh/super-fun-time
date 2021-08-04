# 옵저버 패턴과 리액트

MobX에서 사용하는 개념중에 observable이라는 개념이 존재하고 옵저버 패턴이 사용되는 경우가 많은것 같아 조사를 해보았다.

우리가 언제나 사용하는 리액트도 일종의 옵저버 패턴을 따르는데

컴포넌트들이 스테이트를 props 구독하고, 스테이트가 바뀔때마다 구독하는 모든 컴포넌트들이 re-render가 된다는 점에서 그렇게 이해할 수 있다.

[https://webdevstudios.com/2019/02/19/observable-pattern-in-javascript/](https://webdevstudios.com/2019/02/19/observable-pattern-in-javascript/) \*바닐라 자바스크립트와 옵저버 패턴을 사용해 리액트같이 스테이트가 바뀔때 마다 컴포넌트가 업데이트 되는 설계를 한 가이드

옵저버 패턴을 볼때마다 이해가 잘 안되었던게 어떻게 Observer가 Subject의 변화를 아는지에 대해서였는데

결국에 Subject에서 Observer들의 묶음을 가지고 있고, Subject에 변화가 있을때 "notify"를 통해 Observer의 "update" 함수를 다 실행 시켜주는 것이었다.

Implementation 마다 차이가 있겠지만 옵저버 패턴의 작동법을 대략적으로 파악할 수 있었던 것 같다.

[돌아가기](/README.md)
