# 01-01 typescript 란
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

# 01-02 typescript 설치 및 사용
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

# 03-01 컴파일 옵션
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


# 03-02 structural type system vs nominal type system
- structural type system
    - 구조가 같으면, 같은 타입이다.

```javascript
interface IPerson{
    name: string;
    age: number;
    speak(): string;
}
type PersonType ={
    name: string;
    age: number;
    speak(): string;
}
let personInterface: IPerson = {} as any;
let personType: PersonType = {} as any;

personInterface = personType;
personType = personInterface;
```

- nominal type system (java, c)
    - 구조 형태가 같아도 이름이 다르면, 다른 타입이다.

- duck typing (파이썬)
    - 런타임에서 발생하는 타이핑 방식
    - 만약 어떤 새가 오리처럼 걷고, 헤엄치고, 꽥꽥거리는 소리를 낸다면 나는 그 새를 오리라고 부를 것이다.

# 3-3 타입 호환성 (type compatibility)
```javascript
let sub1: 1 = 1;
let sup1: number = sub1;
sub1 = sup1 // error

let sub2: number[] = [1];
let sup2: object = sub2;
sub2 = sup2; // error

let sub3: [number, number] = [1, 2];
let sup3: number[] = sub3;
sub3 = sup3; // error

let sub4: number = 1;
let sup4: any = sub4;
sub4 = sup4 // 에러가 아니다!

let sub5: never = 0 as never;
let sup5: number = sub5;
sub5 = sup5; // error

class Animal{}
class Dog extends Animal{
    eat(){}
}

let sub6: Dog = new Dog();
let sup6: Animal = sub6;
sub6 = sup6 // error
```

- 같거나 서브 타입인 경우, 할당이 가능하다.
- 함수의 매개변수 타입만 같거나 슈퍼타입인 경우, 할당이 가능하다.

# 3-4 타입 별칭 (type alias)
- 타입 별칭
    - interface랑 비슷해 보인다.
    - primitive, union type, tuple, function
    - 기타 직접 작성해야 하는 타입을 다른 이름을 지정할 수 있다.
    - 만들어진 타입의 refer로 사용하는 것이지, 타입을 만드는 것은 아니다.

- aliasing primitive
```typescript
type MyStringType = string;
const str = 'world';
let myStr: MyStringType = 'hello'
myStr = str;
```


- aliasing union type
```typescript
let person: string | number = 0;
person = 'Mark'
type StringOrNumber = string | number;
let another: StringOrNumber = 0;
another = 'Anna'
```

- alias vs interface
    - 타입이 타입으로서 목적, 존재 가치가 명확할 때 -> interface
    - 단순 대상을 가리킬 뿐이거나, 별명으로서 존재 -> type alias
    - 기술적으로 차이도 있다.

# 4-1 compilation context
- 어떤 파일을 변환할 지
- 변환할 때 어떤 컴파일 옵션을 사용할 지
- tsconfig.json 을 통해 설정 가능하다.

# 4-2 tsconfig schema
- top level properties
    - compileOnSave
    - extends
    - compileOptions
    - files
    - include
    - exclude
    - references

# 4-3 complieOnSave
- "compileOnSave": true 
    - 파일을 저장하면 컴파일
    - 누가?
        - Visual Studoi 2015 with TypeScript 1.8.4 이상
        - atom-typescript 플러그인

# 4-4 extends
- 다른 파일을 상속받을 수 있다.
- npm 패키지들중 base 패키지를 다운 받아서 상속할 수도 있다.

# 4-5 files, include, exclude 
- 중요하다
- 어떤 파일들을 컴파일할지 결정한다.
- files 의 세팅 값 우선순위가 가장 높다.
    - exclude로 제외 하더라도 포함한다.
- exclude
    - include 안에 포함된건 제외하더라도 files 안의 파일은 제외할 수 없다.
    - 설정 안하면 4가지(node_modules, bower_components, jspm_pacakges, <outDir>)를 default로 제외한다.
        - <outDir>: 컴파일한 결과물을 저장하는 폴더
- include
    - files나 include에 있지 않으면 포함한다. 
    - * 같은걸 사용하면, .ts/ .tsx/ .d.ts만 include (allowJS)


# 4-6 compileOptions - typeRoots, types
- 타이핑이 안되어 있는 다른 라이브러리를 사용할 때, 타입을 지정
- 이전에는 서드파티를 이용해 제공하고 있었다.
- @types -> typescript 2.0부터 추가된 기능
    - 외부 자바스크립트 라이브러리에 대한 타입을 패키지화 시켜서 tsconfig안에서 사용할 수 있도록 해줌
- node_modules/@types 폴더에 설치됨
- typeRoots -> 기본적으로 아무 설정을 안하면, 이름과 똑같은 node_modules/@types/<이름> 폴더를 가서 찾는다.
- 배열을 통해 다른 폴더도 지정 가능하다.
- 모든 모듈이 @types로 되어 있으면 좋겠지만, 유명하지 않은 모듈은 그런게 잘 안되어 있을 수도 있다.
    - 나만의 @types를 지정할 폴더를 정해줄 수 있다.
- types
    - 패키지의 경로가 아닌 이름을 쓰는것이다.
- @types
    - 아무 설정을 안하면 -> node_modules/@types
    - typeRoots를 사용하면
        - 배열 
    - types를 사용하면
        - 배열 안의 모듈 혹은 ./node_modules/@types/ 안의 모듈 이름에서 찾아온다.
        - []를 넣는다는건 이 시스템을 이용하지 않겠다는 것이다.
    - typeRoots와 types는 같이 사용하지 않는다.

# 4-7 compileOptions - target, lib
- target
    - 어떤 런타임에서 실행 할 지
    - target으로 컴파일 된다.
    - default: ES3
    - 빌드의 결과물을 어떤 버전으로 할 것이냐.
- lib
    - 작성하는 코드는 실행 환경에 맞게 type definiton이 지정되어 있어야 한다.
    - 내가 실행하고자 하는 환경에 맞게 기본 타입을 저장한다. (browser, node, ...)
    - 타입스크립트가 설치 될 때, 그 안에 번들되어 있는 declaration files 중에 어떤 것을 쓸 지 정할 수 있다.
    - 일반적으로 target에 따라 lib가 지정된다.
    - console.log
        - 아무 지정 안하면 -> lib.dom.d.ts
        - [] 를 넣으면 -> lib에 아무것도 지정하지 않았기에, 무엇인지 모르는 상태에 놓인다.
    - 기본 type defninition 라이브러리를 어떤 것으로 사용할 것이냐.
    - lib을 지정하지 않을 때,
        - target이 'es3'면, default로 lib.d.ts를 사용
        - target이 'es5'면, default로 dom, es5, scripthost를 사용
        - target이 'es6'면, default로 dom, es6, dom.iterable, scripthost를 사용
    - lib을 지정하면 그 lib 배열로만 라이브러리를 사용한다.
        - 빈[] -> no definition found

# 4-8 compileOptions - outDir, outFile, rootDir
- outFile
    - amd(require.js) 를 사용할 때 하나의 파일로 만들어준다.
    - commonjs, es6로는 할 수 없다.
- outDir
    - 컴파일된 결과물의 root directory 지정
- rootDir
    - rootDir 로 지정된 곳부터 만나는 ts파일을 컴파일 한다.
    - 똑같은 하이라이키를 가지고 outDir 폴더에 생성된다.
    - 지정하지 않으면, root directory에서 가장 처음 만나는 ts 파일이 있는 곳 부터 컴파일을 시작한다.

# 4-8 compileOptions - strict
- 무조건 true로 설정 하는 것이 기본이다.
- 왜 켜야 하는가?
    - 엄격하게 타입을 체크하는 옵션을 킨다.
- noImplicitAny
    - 개발자가 any를 직접 지정해야 한다.
- noImplicitThis
    - this를 명시적으로 사용해야 한다.
    - 함수의 첫 번째 인자를 this로 지정할 수 있다.
        - 타입스크립트에만 있는 문법이다.
        - this의 타이핑을 해줘야 한다.
        - call, apply, bind 와 같이 this를 대체하여 함수 콜을 하는 용도로 쓰인다.
    - class에서는 this를 사용하면서, noImplicitThis와 관련한 에러가 나지 않는다. (당연)
    - class에서 constrcutor를 제외한 멤버 함수의 첫번째 매개변수도 일반 함수와 마찬가지로 this를 사용할 수 있다. 
- strictNullChecks
    - 모든 타입에 null이 서브타입으로 포함되는 것을 막을 수 있다.
- strictPropertyInitialization
    - 정의되지 않은 클래스의 속성이 생성자에서 초기화되었는지 알려준다.
    - constructor에서 안하는 경우, 아래처럼 ! 를 이용하면 된다.
    ```typescript
    class Person {
        private _name!: string;
        
        public async initilaize(name: string){
            this._name = name;
        }
    }
    ```
- strictBindCallApply
    - bind, call, apply를 사용 할 때 this의 타입을 지정해야 한다.
- alwaysStrict
    - 각 소스 파일에 대해 strict mode로 코드를 분석한다.
