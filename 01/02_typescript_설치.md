### node.js
- browser에서 자바스크립트를 돌리는데 필요한 엔진을 떼다가 server side에서 쓸 수 있도록 만들어줌
- chrome에 있는 v8 엔진을 이용
- 이 엔진을 이용하여 javascript 를 이용하여 system api를 사용

### browser
- 대표적인 실행 환경
- 브라우저에서 javascript를 해석한다.
- Dom을 제어할 수 있다.

### node.js 설치
- LTS: long term support
- Current: 최신 버전

### node.js version manager
- nvm(node version manager): 필요에 따라 node의 버전을 변경 가능
- n

### typescript 컴파일러 설치
- npm i typescript -g
- tsc source.ts
    - typescript -> javascript
- node source.ts

### tsc --init
- tsc --init 을 이용해 tsconfig.json을 만든다
- tsc만 입력하면 설정대로 컴파일 된다.

### tsc -w
- 파일이 수정 됐을 때 마다 컴파일된다.

### npm uninstall typescript -g
- yarn init
- yarn add typescript
- .\node_modules\.bin\tsc
    - npx tsc (.\node_modules\.bin\ 이 부분이 치환됨)
- .\node_modules\typescript/bin/tsc
- npx tsc 으로 실행 가능
- npx tsc --init
- npx tsc
- pnx tsc -w

### package.json 에서 script로 실행하기
- "build": "tsc"
    - scripts 안에서 사용할 때는 node_modules\.bin 생략 가능
- yarn build
- "build:watch": "tsc -w"
- yarn build:watch