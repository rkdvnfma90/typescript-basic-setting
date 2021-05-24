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
