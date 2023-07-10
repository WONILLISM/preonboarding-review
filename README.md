# 원티드 프리온보딩 인턴십 11차 1주차 리뷰

# lint and formmater 설정

`vite` 빌드 툴을 사용하여서 기본적으로 `eslint`, `eslint-plugin-react-hooks`, `eslint-plugin-react-refresh` 가 기본적으로 내장되어 있다.

강의에서는 기본 `eslint`와 prettier와의 충돌을 막기위한 `eslint-config-prettier` 만 설치했지만, 이 프로젝트에서는 airbnb style guide를 따라보고자 한다.

## eslint 설치

우선적으로 `vite` 빌드 툴로 설치되는 `eslint`들을 알아보자.

- `eslint`
  - 코드 자체의 문법 교정, 코드 스타일링 기능
- `eslint-plugin-react-hooks`
  - React Hook 규칙을 강제해주는 `eslint plugin`
    1. Hook은 최상위(at the Top Level)에서만 호출해야한다.
       - 반복문, 조건문, 중척된 함수에서 호출하면 안됨.
    2. 오직 React 함수 내에서 호출해야 한다.
  - [React 공식문서 - Hooks Rules](https://legacy.reactjs.org/docs/hooks-rules.html)
- `eslint-plugin-react-refresh`
  - 빠른 새로 고침으로 구성 요소를 안전하게 업데이트할 수 있는지 확인합니다.
  - [패키지 Repo](https://github.com/ArnaudBarre/eslint-plugin-react-refresh)

### prettier 설치

`eslint`에도 포매팅 기능이 있지만, 더 강력한 포매터인 `prettier`를 설치하려면, 충돌을 막기 위해 `eslint-config-prettier` 라이브러리를 설치해야 한다.

`yarn add -D prettier eslint-config-prettier`

### scripts 추가

package.json에 아래 명령어들을 추가

```json
  ...
    "lint:fix": "eslint --fix ./src/**/*.{ts,tsx,js,jsx}",
    "prettier": "prettier --write ./src/**/*.{ts,tsx}"
  ...
```
  
# Husky 설정

## Husky를 통한 Git Hook 설정
- `yarn add -D husky`  
   - 최초 진행시 `npx husky install`  

- husky에 등록된 hook을 .git에 적용
```json
// package.json

{
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "lint": "eslint src --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
    "lint:fix": "eslint --fix ./src/**/*.{ts,tsx,js,jsx}",
    "prettier": "prettier --write ./src/**/*.{ts,tsx}",
    "preview": "vite preview",
  },
}
```  

## `pre-commit`, `pre-push` hook 추가

- `npx husky add .husky/pre-commit "yarn run prettier"`
- `npx husky add .husky/pre-push "yarn run lint"`



