# ESLint & prettier (Airbnb Style)

vscode - ESLint & Prettier extension 설치

## 1. ESLint

CRA 프로젝트를 시작했다면 ESLint는 기본적으로 설치된다. 하지만 package.json 에서 

```js
//.eslintrc.js

 "eslintConfig": {
    "extends": "react-app"
  }
```

가 되어있는지 확인한다. -> 에디터에서 ESLint라고 알려주는 것

```
npx install-peerdeps --dev eslint-config-airbnb
```
설치 후 pakage.json 에서 확인 후 세부 설정을 해준다

package.json / .eslintrc.js / .eslintrc.json 중 한 곳에서 config 설정을 해주면 된다.

root 다이렉토리에 .eslintrc.js 파일을 생성해 

```js
module.exports = {
  env : {
    browser : true,
    es6 : true,
    node : true,
  },
  extends : ['airbnb'],
};
```
위와 같이 설정해준다.

## 2. Prettier

```
npm install --save-dev --save-exact prettier
```
코드를 정해진 규칙에 따라 자동으로 정리, 즉 포멧팅 해주는 기능을 제송한다. npm을 통해서 설치가 가능하지만 익스텐션으로 설치했기에 따로 설치할 필요가 없다.

root 디렉토리에 .prettier.json / .prettier.js 파일 중 하나를 생성한다.

```js
//.prettierrc.js

module.exports = {
  singleQuote: true,
  // 문자열은 따옴표로 formatting
  semi: true,
  //코드 마지막에 세미콜른이 있게 formatting
  useTabs: false,
  //탭의 사용을 금하고 스페이스바 사용으로 대체하게 formatting
  tabWidth: 2,
  // 들여쓰기 너비는 2칸
  trailingComma: 'all',
  // 자세한 설명은 구글링이 짱이긴하나 객체나 배열 키:값 뒤에 항상 콤마를 붙히도록 	  	//formatting
  printWidth: 80,
  // 코드 한줄이 maximum 80칸
  arrowParens: 'avoid',
  // 화살표 함수가 하나의 매개변수를 받을 때 괄호를 생략하게 formatting
};
```
로 설정해준다.
이제 매범 저장할 때마다 자동으로 코드를 정리해준다.

이렇게 해도 오류가 사라지지 않는다면
```js
//.eslintrc.js

module.exports = {
  env: {
    browser: true,
    es6: true,
    node: true,
  },
  extends:['airbnb','prettier/react', 'eslint:recommended','plugin:prettier/recommended'],
  // prettier/react 추가
  rules:{
    'react/jsx-filename-extension': 
    ['error', { 'extensions': [".js", ".jsx"] }],
  }
};
```

로 설정해준다. 사용하다가 거슬리는 자잘한 린트에러들은 공식문서를 찾아보고 설정한다. 
마지막으로 ESLint와 Prettier를 마냥 편한 기능으로 생각하지 말고 이런 규칙과 코드 스타일을 눈에 익힐 수 있도록 노력해야한다.

---
ref.
- https://velog.io/@_jouz_ryul/ESLint-Prettier-Airbnb-Style-Guide%EB%A1%9C-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0
- https://www.npmjs.com/package/eslint-config-airbnb