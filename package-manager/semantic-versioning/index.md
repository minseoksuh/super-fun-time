# react-range와 Semantic Versioning

- [https://robertcooper.me/post/how-yarn-lock-files-work-and-upgrading-dependencies](https://robertcooper.me/post/how-yarn-lock-files-work-and-upgrading-dependencies)
- [https://classic.yarnpkg.com/en/docs/selective-version-resolutions/](https://classic.yarnpkg.com/en/docs/selective-version-resolutions/)

최근에 프로젝트를 개발 서버에서 돌릴시, 새로고침 할 때 간헐적으로 react-range 라이브러리 코드에서 오류가 발생했다.
˜
오류 메세지 검색을 했는데 버전업을 하면 해결할 수 있다고 해서 디펜던시 업그레이드를 하려고 하는데

내가 패키지 버전이 정확히 어떻게 돌아가는지 모른다는걸 알았다.

그래서 간단히 정리해보려고 한다.

yarn과 npm 에서 사용하는 Semantic Versioning

## Semantic Versioning 기본

major.minor.patch

- major: 패키지 api 에 breaking, 또는 incompatible한 변경 점이 있을 경우
- minor: 새로운 기능 추가, backwards-compatible
- patch: 버그 픽스, backwards-compatible

- 예를 들어 지금 프로젝트에서 어떤 패키지 버전 1.1.1을 사용하고 있었다고 하면, 1.2.0 이 되거나 1.1.2가 되더라도 오류 없이 코드가 돌아간다는 뜻인 것 같다.

### Version ranges

yarn.lock이 있다면 설치할때 lock에 설정되어 있는 버전을 깔겠지만 lock이
없거나, yarn upgrade를 할 때 버전 범위 안에서 최신을 설치한다.

```js
{
  "dependencies": {
    "package-1": ">=2.0.0 <3.1.4",
    "package-2": "^0.4.2",
    "package-3": "~2.7.1"
  }
}
```

- Comparators: <, >, <= 이런것들로 범위를 나타넴
- Tilde Ranges: ~ (x.y.z 중 z 패치에 대한 버전업은 허용함)
- Caret Ranges: ^ (x.y.z 중 y 패치에 대한 버전업은 허용함, 범위 설정을 명시적으로 안한다면 yarn 기본이 이 설정이라고 함)

그래서

```js
{
  "dependencies": {
    "react-range": "^1.7.0"
  }
}
```

이 패키지를 1.8.9 버전으로 업데이트 해야 버그를 해결할 수 있다면  
명시적으로 버전을 ^1.8.9 이련식으로 고쳐줄 필요 없이
yarn upgrade react-range 만 하면 yarn.lock에서 설치되는 버전이 바뀌고
package.json은 굳이 변경하지 않아도 된다.

## 패키지 버전 충돌 시 어떻게 처리가 되나요

궁금하던게 만약 두 개의 패키지가 다른 버전의 subDependency를 가지고 있다면 npm이나 yarn은 실제로 어떤 버전을 설치하냐 였습니다.

- [https://www.geeksforgeeks.org/how-does-npm-handle-version-conflicts/](https://www.geeksforgeeks.org/how-does-npm-handle-version-conflicts/)

여기에서 보면

패키지 A 와 패키지 B가 설치될때, 몇가지 경우가 있다고 합니다.

1. A와 B 둘다 디펜던시가 없음 > node_modules에 root dependency로 깔림
2. A 는 디펜던시가 없지만 B는 A에 의존함 (버전도 도일) > 그럼 A는 루트에만 설치되고 B의 디펜던시에는 따로 설치 안됨
3. A(v1) 는 디펜던시가 없지만 B는 A(v2)에 의존함 (버전이 다름) > 우선 A(v1)이 루트 디펜던시로 설치가 되고, A(v2)는 B 패키지 내 node_modules에 따로 설치가 됨
4. A(v1) 는 디펜던시가 없지만 B는 A(v2)에 의존함, 다른 패키지 C도 A(v2)에 의존함 (버전이 다름) > 3번의 반응이 우선 일어나고, C 패키지 내에 A(v2)가 따로 설치가 됨. subDependency 끼리에는 버전이 같을 경우 설치 생략하는 로직이 없나봄

[돌아가기](../../README.md)
