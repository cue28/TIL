# Redux-saga

## Redux-saga
액션을 모니터링하고 있다가, 특정 액션이 발생하면 이에 따라 특정 작업을 하는 방식으로 사용한다. 특정 작업이란, 자바스크립트를 실행하는 것 일수도 있고, 다른 액션을 디스패치 하는 것, 현재 상태를 불러오는 것 일수도 있다.

redux-thunk에 비해 다양한 작업들을 할 수 있다.

1. 비동기 작업을 할 때 기존 요청을 취소 처리 할 수 있다.
2. 특정 액션이 발생했을 때 이에 따라 다른 액션이 디스패치되게끔 하거나, 자바스크립트 코드를 실행 할 수 있다.
3. 웹 소켓을 사용하는 경우 channel 이라는 기능을 사용하여 더욱 효율적으로 코드를 관리할 수 있다.
4. API 요청이 실패했을 때 재요청하는 작업을 할 수 있다.

이 외에도 까다로운 비동기 작업들을 처리할 수 있다.

## Generator

조금 생소할 수 있는 [Generator](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Generator) 문법을 사용한다. 핵심 기능은 함수를 작성 할 때 함수를 특정 구간에 멈춰놓을 수도 있고, 원할 때 다시 돌아가게 할 수도 있다. 그리고 결과값을 여러번 반환 할 수도 있다.

```js
function weirdFunction() {
  return 1;
  return 2;
  return 3;
  return 4;
  return 5;
}
```
위 함수는 1을 리턴하고 끝날 것이다. 하지만 제너레이터 함수에서는 함수에서 값을 순차적으로 반환할 수 있다. 흐름을 멈춰놓았다가 나중에 이어서 진행 할수도 있다.
```js
function* generatorFunction() {
    console.log('안녕하세요?');
    yield 1;
    console.log('제너레이터 함수');
    yield 2;
    console.log('function*');
    yield 3;
    return 4;
}
```
이 함수를 만들 때는 `function*` 이라는 키워드를 사용한다. 함수를 호출했을 때는 한 객체가 반환되는데, 이를 `제너레이터`라고 부른다. 
```js
const generator = generatorFunction();
```
`generator.next()` 를 호출해야해만 실행되고, yield 한 값을 반환한 수 코드의 흐름을 멈춘다. 다시 `generator.next()` 를 호출하면 흐름이 이어서 다시 시작된다. (오 ..!)
```js
function* sumGenerator() {
    console.log('sumGenerator이 시작됐습니다.');
    let a = yield;
    console.log('a값을 받았습니다.');
    let b = yield;
    console.log('b값을 받았습니다.');
    yield a + b;
}
```
`next`를 호출 할 때 인자를 전달하여 제네레이터 함수 내부에서 사용할 수도 있다.

그렇다면 Generator로 어떻게 액션 모니터링이 일어날까?
```js
function* watchGenerator() {
    console.log('모니터링 시작!');
    while(true) {
        const action = yield;
        if (action.type === 'HELLO') {
            console.log('안녕하세요?');
        }
        if (action.type === 'BYE') {
            console.log('안녕히가세요.');
        }
    }
}

const watch = watchGenerator();
watch.next({type:'HELLO'}) //안녕하세요?
```
이러한 원리로 액션을 모니터링하고, 특정 액션이 발생했을 때 원하는 자바스크립트 코드를 실행시켜준다.


https://react.vlpt.us/redux-middleware/10-redux-saga.html