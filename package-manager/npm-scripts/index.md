# npm scripts

npm 스크립트를 확실히 모르는 부분이 있어서 조사해 보았습니다.

## script:somthing

우선 자주 보이는 이런 형태의 문법은 npm 내장 지원은 아니고
특정 script를 더 세분화해서 나누는 naming 컨벤션 같은 거라고 합니다.
npm-run-all 같은 라이브러리를 사용해 같이 실행되기도 합니다.

## Pre & Post Scripts

pre와 post를 사용해서 script 처리 전 후에 행동을 특정할 수 있습니다.

```json
{
  "scripts": {
    "precompress": "{{ executes BEFORE the `compress` script }}",
    "compress": "{{ run command to compress files }}",
    "postcompress": "{{ executes AFTER `compress` script }}"
  }
}
```

npm run compress를 하면 저 순서대로 다 실행된다고 합니다.

## Life Cycle Scripts

특정 상황에만 실행되는 특수 라이프사이클 스크립트.

- prepare: 패키지가 패킹 되기 전에 실행된다 (npm publish, npm pack 등. 기존 prepublish 동작)
- prepublish(deprecated)
- prepublishOnly: npm publish 전에만 사용됨
- prepack: tarball이 패킹 되기 전 실행
- postpack: tarball이 만들어지고 최종 목적지로 이동되기 전 실행됨

## Environment

스크립트가 실행되는 환경 (process 상태, npm 세팅 등)

### path

실행 가능한 스크립트를 정의하는 모듈을 의존하고 있다면,
그 스크립트들은 PATH에 등록이 되서 사용가능해진다고 함.

```json
{
  "name": "foo",
  "dependencies": {
    "bar": "0.1.x"
  },
  "scripts": {
    "start": "bar ./test"
  }
}
```

bar 스크립트를 start에서 사용하고 있음

### package.json vars

package.json 내부 필드들을 앞에 `npm_package_` prefix를 붙여서 접근가능함.

> You can access these variables in your code with process.env.npm_package_name and process.env.npm_package_version, and so on for other fields.

### configuration

config 파라메터가 `npm_config_` prefix를 통해 확인 가능함

### current lifecycle event

`npm_lifecycle_event` 변수가 현재 도는 사이클로 설정이 됩니다.
현재 어떤 사이클 중인지 알아야 할 때 쓰면 될듯.

## Exiting

script가 0말고 다른 코드로 exit 된다면, 프로세스가 중단됨.

`echo \"Error: no test specified\" && exit 1`

## Hook Scripts

lifecycle 이벤트에 훅을 달아놓을 수 있습니다.

`node_modules/.hooks/{eventname}`

여기에 해당 이벤트명으로 등록해 놓으면 불린다고함.

## Best Practices

- Don't exit with a non-zero error code unless you really mean it.

- Try not to use scripts to do what npm can do for you.

- Inspect the env to determine where to put things.

- Don't prefix your script commands with "sudo".

- Don't use install
  > Use a .gyp file for compilation, and prepublish for anything else. You should almost never have to explicitly set a preinstall or install script.

## Reference

[https://docs.npmjs.com/cli/v7/using-npm/scripts](https://docs.npmjs.com/cli/v7/using-npm/scripts)

[돌아가기](/README.md)
