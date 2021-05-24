# 타입스크립트 기본 설정

## 절차

1. `npm init -y` 로 프로젝트 초기화를 설정한다.
2. `npm i typescript -D` Dev Dependencies 에 타입스크립트를 설치한다.
3. `npx tsc --init` 타입스크립트 기본 설정으로 `tsconfig.json` 파일이 생성된다.

<br/>
<br/>

## top-level properties

- `compileOnSave` : 파일 저장시 자동 컴파일 여부 (boolean) default 값은 false 이다. 단 모든 환경에서 되는 것이 아니라 VisualStudioCode 에서는 `VSC 2015 with Typescript 1.8.4 이상` 일 때 가능하다.
