# 타입스크립트 기본 설정

## 절차

1. `npm init -y` 로 프로젝트 초기화를 설정한다.
2. `npm i typescript -D` Dev Dependencies 에 타입스크립트를 설치한다.
3. `npx tsc --init` 타입스크립트 기본 설정으로 `tsconfig.json` 파일이 생성된다.

<br/>
<br/>

## top-level properties

- `compileOnSave` : 파일 저장시 자동 컴파일 여부 (boolean) default 값은 false 이다. 단 모든 환경에서 되는 것이 아니라 VisualStudioCode 에서는 `VSC 2015 with Typescript 1.8.4 이상` 일 때 가능하다.

- `extends` : tsconfig 파일에서 다른 파일을 상속받아 설정할 수 있고, 타입스크립트 `버전 2.1 이상` 에서 사용할 수 있다. 설정값은 상대경로를 입력한다.

- `files` : 컴파일 할 대상들을 지정한다. `exclude`에 지정되어 있는 파일이라도 `files`에 있다면 컴파일 한다. (fiels의 우선순위가 exclude보다 높음)

- `include` : 컴파일 할 대상들을 지정한다. (glob 패턴). `*`를 사용하면 .ts, .tsx, .d.ts만 include 한다 (allowJS).

- `exclude` : 컴파일 제외할 대상들을 지정한다. (glob 패턴). 만약 설정을 하지 않으면 4가지 (node_modules, bower_components, jspm_packages, \<outDir>)를 default 로 제외한다. \<outDir>는 include에 있다고 하여도 항상 제외한다.

- `compileOptions`

  - `typeRoots` : 배열 안에 들어있는 경로들 아래서만 가져와 사용한다.
  - `types`: 외부 라이브러리 (e.g. react)에 대한 타이핑을 도와주는 기능. 아무 설정을 하지 않으면 `node_modules/@types` 라는 모든 경로를 사용한다. 만약 빈 배열 `[]`로 설정하면 사용하지 않는 다는 의미이다. `typeRoots`와 `types`를 같이 사용하지 않는다.
  - `target` : 빌드 결과물의 ECMAScript 버전을 지정한다. default 값은 `ES3` 이다.
  - `lib` : 기본 type definition 라이브러리를 지정한다. lib를 지정하지 않으면 ECMAScript 버전에 따라 default 값이 달라진다. lib를 지정하면 지정한 값들로만 라이브러리를 사용한다.
  - `outDir` : 컴파일된 결과물의 위치
  - `rootDir` : 기준점이 되는 경로 지정 보통 src를 지정함
  - `strict` : 엄격하게 타입을 확인하는 옵션 설정

        - `--noImplicitAny` : 명시적이지 않게 any 타입으로 추론되었을 때 에러발생 여부
        - `--noImplicitThis` : 명시적이기 않게 any 타입을 사용하여 this 표현식에 사용했을 때 에러발생 여부

        ```javascript
        // 첫번째 매개변수에 this를 넣고, this에 타입을 표시하지 않으면 에러가 발생한다.
        // javascript에서는 매개변수에 this를 넣으면 이미 예약된 키워드 이기 때문에 SyntaxError가 발생한다.
        // call / apply / bind와 같이 this를 대체하여 함수 호출을 하는 용도로도 쓰인다.
        function noImplicitThisTest(this, name:string, age:number) {
          this.name = name;
          this.age = age;

          return this;
        }
        ```

        - `--strictNullChecks` : 이 옵션을 키지 않으면 모든 타입에 `null과 undefined`가 포함된 상태로 사용하는 것이다. 그러므로 꼭 켜주자. 만약 키지 않으면 아래처럼 union type을 사용하여 직접 명시를 해줘야 한다.

        ```javascript
        const c: number | null = null;
        ```

        - `--strictFunctionTypes` : 함수의 매개변수 타입이 반공변적 동작 여부 설정
        ```javascript
        // 공변성
        let array: Array<string | number> = [];

        let stringArray: Array<string> = [];
        array = stringArray; // OK
        stringArray = array; // Error

        // 반공변성
        type Logger<T> = (param: T) => void;
        let log: Logger<string | number> = (param) => {
          console.log(param);
        };
        let logNumber: Logger<number> = (param) => {
          console.log(param);
        };
        log = logNumber; // Error
        logNumber = log; // OK

        ```

        -`--strictPropertyInitialization`: 정의되지않은 클래스의 속성이 생성자에서 초기화 되었는지 확인한다. 이 옵션을 사용하려면 `--strictNullChecks` 옵션을 사용해야 한다.
        -`--strictBindCallApply`: bind, call, apply에 대해 더 엄격하게 체크한다.
