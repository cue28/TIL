# 15. let, const 키워드와 블록 레벨 스코프

## 15.1 var 키워드로 선언한 변수의 문제점

ES5까지 변수를 선언할 수 있는 유일한 방법이었던 var의 특징
- 변수 중복 선언 허용 : 의도치 않은 먼저 선언된 변수 값이 변경되는 부작용 발생

  ```js
  var x = 1;
  var y = 1;

  //같은 스코프 내 중복 선언 허용
  //초기화문(변수 선언과 동시에 초기갑을 할당하는 문)이 있는 경우 var 키워드가 없는 것처럼 동작
  var x = 100;
  //초기화문이 없는 변수 선언문은 무시, 에러 X
  var y;

  console.log(x); //100
  console.log(y); //1
  ```
- 함수 레벨 스코프 : 전역 변수를 남발할 가능성이 높아 의도치 않게 전역 변수가 중복 선언되는 경우 발생
  ```js
  var x = 1;

  if (true) {
    //x는 전역변수, 이미 선언된 전역 변수 x가 있으므로 x변수는 중복 선언된다.
    //의도치 않게 변수값이 변경되는 부작용 발생
    var x = 10;
  }

  console.log(x); //10
  ```
  ```js
  var i = 10;

  //i는 전역 변수, 이미 선언된 전역 변수가 i가 있으므로 중복 선언된다.
  for(var i = 0; i < 5; i++){
      console.log(i); //0 1 2 3 4 
  }

  //의도치 않은 값의 변경
  console.log(i); //5
  ```
- 변수 호이스팅 : 에러 X, 프로그램의 흐름상 맞지 않고 가독성이 떨어지며 오류를 발생 가능성이 있음.
  ```js
  //이 시점에서 변수 호이스팅에 의해 이미 foo 변수가 성언됨 (1.선언단계)
  //변수 foo는 undefined로 초기화 (2.초기화 단계) 
  console.log(foo); //undefined

  //변수에 값을 할당 (3.할당 단계)
  foo = 123;

  console.log(foo); //123

  //변수 선언은 런타임 이전에 자바스크립트 엔진에 의해 암묵적으로 실행
  var foo;
  ```

## 15.2 let 

var를 보완하기 위해 ES6에서 새로운 변수 선언 키워드로 let과 const를 도입했다. var 키워드와의 차이점을 중심으로 비교해보자.

- 변수 중복 선언 금지
  - 같은 스코프 내에서 중복 선언을 허용하지 않는다.
  - let 키워드로 중복 선언하면 문법 에러 (SyntaxError: Identifier 'bar' has already been declared)
- 블록 레벨 스코프
  - 함수, if문, for문, while문, try/catch문 등을 지역 스코프로 인정
    ```js
    //전역 스코프
    let foo = 1; //전역 변수

    function foo(){ 
      //함수 스코프
      let foo = 2; //지역 변수
      let bar = 3; //지역 변수
      for(let i = 0; i < 3; i++) {
        //블록 레벨 스코프
        console.log(i); //0 1 2
      }
      console.log(foo); //2
    }

    foo();

    console.log(foo); //1
    console.log(bar); //ReferenceError: bar is not defined
    ```
- 변수 호이스팅
  - 발생하지 않는 것처럼 동작한다.
  - `선언 단계`와 `초기화 단계`가 분리되어 진행된다. 각 생명주기는 다음과 같다.
    ```
    var
             선언 단계 & 초기화 단계 : foo === undefined
    var foo;
    foo = 1; 할당 단계 foo === 1; 

    let
             선언 단계
             일시적 사각지대
    let foo; 초기화 단계 foo === undefined
    foo = 1; 할당 단계 foo === 1
    ```
  - 런타임 이전에 자바스크립트 엔진에 의해 암묵적으로 선언 단계가 먼저 실행되지만, 초기화 단계는 변수 선언문에 도달했을 때 실행된다.
  - 스코프의 시작 시점부터 초기화 단계 시작 지점(변수 선언문)까지 변수를 참조할 수 없는 구간을 `일시적 사각지대(Temporal Deed Zone:TDZ)`이라고 부른다.
    ```js
    //런타임 이전에 선언 단계가 실행, 아직 변수가 초기화되지 않음.
    //초기화 이전의 일시적 사각지대에서는 변수를 참조할 수 없음.
    console.log(foo); // ReferenceError: foo is not defined

    let foo; //변수 선언문에서 초기화 단계가 실행
    console.log(foo); //undefined

    foo = 1; //할당문에서 할당 단계가 실행
    console.log(foo); //1
    ```
    
    ```js
    let foo = 1; //전역 변수
    {
      console.log(foo); //ReferenceError: Cannot access 'foo' before initialization
      let foo = 2; //지역 변수
    }
    ```
    위의 경우에는 호이스팅이 발생하지 않는다면 전역 변수 foo의 값을 출력해야 한다. 하지만 let 키워드로 선언한 변수도 여전히 호이스팅이 발생하기 때문에 참조 에러가 발생한다.

    ES6에서 도입된 let, const 등 모든 선언을 호이스팅한다. 단, let, const, class를 사용한 선언문은 호이스팅이 발생하지 않는 것처럼 동작한다.

- 전역 객체와 let
  - var 키워드로 선언한 전역 변수는 전역 객체 window의 프로퍼티가 된다. 전역 객체의 프로퍼티를 참조할 때 window를 생략할 수 있다.
    ```js
    var x = 1;
    
    function foo(){
      console.log(window.x); //1
      console.log(x); //1
    }
    ```
  - let 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니다. 
    ```js
    let x = 1;
    
    console.log(window.x); //undefined
    console.log(x); //1
    ```

## 15.3 const 키워드

상수(constant)를 선언하기 위해 사용한다. 반드시 그렇지는 않는다. const는 let과 대부분 동일하므로 let 키워드와 차이점을 위주로 살펴보자.

- 선언과 초기화
  - const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화해야 한다. (SyntaxError: Missing initializer in const declaration)
- 재할당 금지
  - var, let 키워드로 선언한 변수는 재할당이 자유로우나 const 키워드로 선언한 변수는 재할당이 금지된다. ( TypeError: Assignment to constant variable.)
- 상수
  - 변수의 상대 개념으로 '재할당이 금지된 변수'를 말한다.
  - const 키워드로 선언한 변수의 원시 값은 변경이 불가능한 값이므로 상수를 표현하는 데 사용된다.
  - 상태 유지와 가독성, 유지보수의 편의를 위해 적극적으로 사용해야한다. 예를 들면, Tax
      ```js
      //세율의 의미하는 0.1은 변경할 수 없는 상수로 활용
      //변수 이름을 대문자로 선언해 상수임을 명확히 나타냄.
      //여러 단어로 이뤄진 경우 언더스코어(_)로 구분해서 스네이크 케이스로 표현
      const TAX_RATE = 0.1;

      //세전
      let preTaxPrice = 100;

      //세후
      let afterTaxPrice = preTaxPrice + (preTaxPrice * TAX_RATE);

      console.log(afterTaxPrice); //110
      ```
- const 키워드와 객체
  - 객체를 할당한 경우 값을 변경할 수 있다.
  - 변경 불가능한 값인 원시 값은 재할당 없이 변경(교체)할 수 있는 방법이 없지만 변경 가능한 값인 객체는 재할당 없이도 직접 변경이 가능하기 때문이다.
  - 재할당을 금지할 뿐 '불변'을 의미하지는 않는다. (11.1.1 참고)
  - 프로퍼티 값의 변경을 통해 객체를 변경하는 것은 가능하다.
  - 이때 객체가 변경되더라도 변수에 할당된 참조값은 변경되지 않는다.
      ```js
      const person = {
        name : 'Lee'
      }

      person.name = 'Kim';

      console.log(person); //{name : 'kim'} 
      ```

## 15.4 var vs. let vs. const
- 변수 선언은 기본적으로 `const`를 사용하고, let은 재할당이 필요한 경우에 한정해 사용하는 것이 좋다.
- const 키워드가 의도치 않은 재할당을 방지하기 때문에 좀 더 안전하다.
- ES6를 사용한다면 var 키워드는 사용하지 않는다.
- 재할당이 필요한 경우에 한정해 let 키워드를 사용한다. 변수의 스코프는 최대한 좁게 만든다.
- 읽기 전용으로 사용하는 원시갑과 객체에는 const 키워드를 사용한다.