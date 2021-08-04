# declare는 왜 사용하나요

[https://stackoverflow.com/questions/43335962/purpose-of-declare-keyword-in-typescript](https://stackoverflow.com/questions/43335962/purpose-of-declare-keyword-in-typescript)

## Answer 1

타입이 작성되지 않은 자바스크립트 코드를 타입스크립트 프로젝트에서 사용해야 하는 경우 declare를 통해 이미 존재하는 코드에 대한 타입을 추가할 수 있다.

## Answer 2

> declare is used to tell the compiler "this thing (usually a variable) exists already, and therefore can be referenced by other code, also there is no need to compile this statement into any JavaScript".

- declare는 ts 컴파일러에게 "이것"은 이미 존재한다고 알려줌
- 그러므로 "이것"은 다른 것들에게 정상적으로 참조될 수 있음
- 이 코드는 자바스크립트로 컴파일할 필요 없음

## TMS

```ts
declare namespace NodeJS {
  export interface ProcessEnv {
    ENV: "local" | "dev1" | "qa1" | "qa2" | "qa3" | "prod" | "prod-beta";
    API_BASE_PATH: string;
    OAUTH_BASE_PATH: string;
    OAUTH_CLIENT_ID: string;
    OAUTH_CLIENT_SECRET: string;
    GOOGLE_ANALYTICS_TRACKING_ID: string;
    NCP_CLIENT_ID: string;
    NCP_CLIENT_SECRET: string;
    NODE_ENV: string;
    FEATURE_CONTEXT?: string;
    SENTRY_DSN: string;
  }
}
```

TMS 내에 사용되는 위 코드를 보면, 빌드 타이밍에 process env에 스크립트로 위 프라퍼티들을 설정해 주는데,  
타입스크립트 컴파일러는 그것을 모르기 때문에 해당 프라퍼티에 그냥 접근하려고 하면 오류로 처리됨.  
그것에 대응하기 위한 코드라고 볼 수 있겠다.

보통 @types/module 패키지에서 module 내 자바스크립트 코드에 대한 타입 정의를 해주기 위해 사용됨.

[돌아가기](/README.md)
