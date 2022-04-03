# 01-01
- Typed Javascript at any scale
    - typescript extends javascript by adding types

- Typescript = language
    - typed superset of javascript
    - compiles to plain javascript
    - 타입스크립트는 programming lanauge 이다.
    - 타입스크립트는 Compiled language 이다.
        - 전통적인 compiled language와 다른 점이 많아 transpile이라는 용어를 사용하기도 한다.
    - 바로바로 실행 가능한 interpreted langaue인 javascript로 만든다.
    - typescript compiler를 이용하여 javascript로 변환해야 한다.

# 01-02
- node.js
    - browser에서 자바스크립트를 돌리는데 필요한 엔진을 떼다가 server side에서 쓸 수 있도록 만들어줌
    - chrome에 있는 v8 엔진을 이용
    - 이 엔진을 이용하여 javascript 를 이용하여 system api를 사용

- browser
    - 대표적인 실행 환경
    - 브라우저에서 javascript를 해석한다.
    - Dom을 제어할 수 있다.

- node.js 설치
    - LTS: long term support
    - Current: 최신 버전

- node.js version manager
    - nvm(node version manager): 필요에 따라 node의 버전을 변경 가능
    - n

- typescript 컴파일러 설치
    - npm i typescript -g
    - tsc source.ts
        - typescript -> javascript
    - node source.ts

- tsc --init
    - tsc --init 을 이용해 tsconfig.json을 만든다
    - tsc만 입력하면 설정대로 컴파일 된다.

- tsc -w
    - 파일이 수정 됐을 때 마다 컴파일된다.

- npm uninstall typescript -g
    - yarn init
    - yarn add typescript
    - .\node_modules\.bin\tsc
        - npx tsc (.\node_modules\.bin\ 이 부분이 치환됨)
    - .\node_modules\typescript/bin/tsc
    - npx tsc 으로 실행 가능
    - npx tsc --init
    - npx tsc
    - pnx tsc -w

- package.json 에서 script로 실행하기
    - "build": "tsc"
        - scripts 안에서 사용할 때는 node_modules\.bin 생략 가능
    - yarn build
    - "build:watch": "tsc -w"
    - yarn build:watch

# 02-02 primivite types
- 래퍼 객체로 만드는 것을 권장하지 않는다.
```
new Boolean(false); // typeof new Boolean(false) : "object"
new String('wolrd'); // typeof new String('wolrd') : "object"
new Number(42); // typeof new Number(42) : "object"
```
# 02-04 number
- NaN과 1_000_000 도 number이다.
    - let notANumber: number = NaN;
    - let underscoreNum: number = 1_000_000;

# 02-06 symbol
- 주로 접근을 제어하는데 쓰인다
```
const sym = Symbol();
const obj = {
    [sym]: "value"
}
obj[sym]
```

# 02-07 null & undefined
- undefined & null are subtypes of all other types
    - --stckitNullChecks를 사용해서 primitive type의 subtypes로 사용하지 못하게 할 수 있다.

- null
    - 무언가가 있는데, 사용할 준비가 덜 된 상태.

- undefined
    - 값을 할당하지 않은 변수가 갖는 값
    - 무언가가 아예 준비가 안된 상태
    - object의 property가 없을 때도 undefined 이다.
    - void 타입에 undefined를 넣을 수 있다.

# 02-08 object
- object
    - primitive type이 아닌 것을 나타내고 싶을 때 사용하는 타입

# 02-12 unknown
- unknown
    - 모르는 변수 타입을 묘사해야 할 수도 있다.
    - any 보다 type-safe한 타입
    - 컴파일러가 타입을 추론 할 수 있게끔 타입의 유형을 좁힐 수 있다.
    - 타입을 확정해주지 않으면 다른 곳에 할당 할 수 없고, 사용할 수 없다.

# 02-12 never
- never
    - never 타입은 모든 타입의 subtype이며, 모든 타입에 할당 할 수 있다.
    - 하지만, never 에는 그 어떤 것도 할당할 수 없다.
    - any 조차도 never에 할당할 수 없다.
    - 잘못된 타입을 넣는 실수를 막고자 할 때 사용한다.

# 03-01
- 타입
    - 타입을 명시적으로 지정할 수 있다.
    - 타입을 명시적으로 지정하지 않으면, 타입스크립트 컴파일러가 자동으로 타입을 추론한다.

- noImplicityAny 옵션
    - 명시적으로 지정되지 않은 any 를 막아준다.

- strictNullChecks 옵션
    - 모든 타입에 자동으로 포함되어 있는 null, undefined를 제거해준다.
```
function f(a: number){
    if(a>0){
        return a * 38
    }
}
// return 값은 number | undefined로 추론된다.
```

- noImplicitReturns
    - 함수 내에서 모든 코드가 값을 리턴하지 않으면 컴파일 에러를 발생 시킨다.

