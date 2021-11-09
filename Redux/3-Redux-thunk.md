# Redux-thunk

thunk란, 특정 작업을 할 수 있도록 비동기 처리(미루기) 위해 함수 형태로 감싼 것을 의미한다. 기본 리덕스는 action객체를 dispatch하여 reducer에 전달한다. thunk는 action 뿐만 아니라 thunk 함수를 만들어 dispatch할 수 있다. 다시 말해, action 안에 type과 payload, API 요청이나 비동기 처리 로직도 함께 들어갈 수 있다.

1번 파일에서 작성한 코드는 파이널 프로젝트에서 redux-thunk 코드를 가져온 것이다.

기존의 동기적인 로직을 처리하는 방식과 다르지 않지만, 경우에 따라 객체를 반환하거나, 함수를 반환하기도해서 이러한 유연성이 action을 복잡하게 만든다는 단점이 존재한다. 또한, 내부적으로 시작할 때, 성공했을 때, 실패했을 때마다 액션을 patch해주어야해서 번거로움이 존재한다.

redux-saga는 이러한 중복 액션에 대한 비동기 처리를 쉽게 해결해준다.

https://redux-advanced.vlpt.us/2/01.html
https://github.com/reduxjs/redux-thunk