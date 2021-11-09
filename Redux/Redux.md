# Redux : A predictable state conrainer for Javascript apps

### Redux의 필요성

→ 자식 컴포넌트에서 다른 자식 컴포넌트로 state를 전달해줄 때, 부모 컴포넌트에 끌어올리기를 하여 사용한다. 한 두가지의 컴포넌트라면 괜찮지만, 수백개의 컴포넌트라면 상태관리는 매우 복잡해진다. 이에 Redux를 이용한면 **상태관리에 용이**해진다. 

→ 한마디로 하나의 상태로 (state = {}) 외부로부터 철저히 보호시켜 수정이 안되게 관리한다.

### **장점**

➀ 상태를 예측 가능하게 만들어준다.

➁ 유지보수

➂ 디버깅에 유리하다(action과 state log기록 시)

➃ 테스트를 붙이기 쉽다.

### **Redux의 3가지 원칙**

➀ 항상 같은 곳에서 항상 동일한 데이터를 가지고 온다.

➁ state는 읽기 전용이다.

➂ 변경은 순수함수로만 가능하다.

![redux](https://cdn.discordapp.com/attachments/900742245920166020/907554909401018388/unknown.png)

- **Store** : 상태가 관리되는 오직 한 공간 store 안에 필요한 state를 두고 스토어 안에 접근해서 가지고 온다.
- **Action** : JS 객체 store에 state를 운반하는 역할을 하며, 하나의 객체로 표현된다.

함수를 생성해 아래 객체를 리턴하여 Action을 생성한다.

```js
{
//! type은 필수로 가지고 있어야한다.
  type: "ADD_TODO",
  data: {
    id: 0,
    text: "블로그 작성"
  }
}
```
- **Reducer** : 이 곳을 거쳐 현재 상태와 Action을 이용해 다음 상태를 만들어 낸다.
```js
//! 2가지의 파라미터를 가진다.
const blogReducer = (state = initialState, action) => {
  switch (action.type) {
    case ADD_TO_BLOG:
      return Object.assign({}, state, {
        blogcontent: [...state.blogcontent, action.payload]
      })
    default:
      return state;
  }
}
```
Reducer의 Immutability(불변성) 때문에 복사해서 사용한다.

**기억하기 !** Action 객체는 Dispatch에게 전달되고, Dispatch는 Reducer를 호출해서 새로운 state를 생성한다.

- **Disfatch** : Action을 전달하는 메소드
- **useSelector()** : 컴포넌트와 state를 연결하는 역할
- **useDispatch()** : Action 객체를 Reducer로 전달해주는 메소드

데이터 변경  : Dispatch, reducer 를 통해 state를 변경할 수 있다.

데이터 사용 : get status 를 사용해 데이터를 가져갈 수 있다.

→ 의도하지 않게 데이터 값을 수정되는 것을 방지할 수 있다.

- index.js
    
    ```jsx
    import React from 'react';
    import App from './App';
    import store from './store/store';
    import { Provider } from 'react-redux';
    
    ReactDom.render(
    **//리덕스 적용하기 : index.js에서 사용하는 하나의 상태**
      <Provider store={store}>
          <App />
      </Provider>,
      document.getElementById('root')
    );
    ```
    
    ```jsx
    import App from './App';
    import './style.css';
    
    import React from 'react';
    import ReactDom from 'react-dom';
    import { BrowserRouter } from 'react-router-dom';
    
    import { Provider } from 'react-redux';
    import store from './redux/store/store';
    import { PersistGate } from 'redux-persist/integration/react';
    import { persistStore } from 'redux-persist';
    
    const persistor = persistStore(store);
    
    ReactDom.render(
      <Provider store={store}>
    		**//새로고침 state 날라가지 않게 하기**
        <PersistGate persistor={persistor}>
          <BrowserRouter>
            <App />
          </BrowserRouter>
        </PersistGate>
      </Provider>,
      document.getElementById('root')
    );
    ```
    
- store
    ```jsx
    //store.js
    **//applyMiddleware : to support asynchronous actions without much boilerplate code or a dependency on a library like Rx.
    //https://redux.js.org/api/applymiddleware**
    import { compose, createStore, applyMiddleware } from 'redux';
    import rootReducer from '../reducers/index';
    **//리덕스에서 비동기 작업을 처리할 때 사용하는 미들웨어, action 함수가 아닌 dispatch 함수를 사용
    //https://react.vlpt.us/redux-middleware/04-redux-thunk.html**
    import thunk from 'redux-thunk';
    
    **//리덕스 개발자도구와 미들웨어를 사용하기 위한 함수**
    const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__
      ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({})
      : compose;
    const store = createStore(
      rootReducer,
      composeEnhancers(applyMiddleware(thunk))
    );
    
    export default store;
    ```
    
    ```jsx
    import { compose, createStore, applyMiddleware } from 'redux';
    import rootReducer from '../reducers/index';
    import thunk from 'redux-thunk';
    import promiseMiddleware from 'redux-promise';
    
    const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__
      ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({})
      : compose;
    const store = createStore(
      rootReducer,
      composeEnhancers(applyMiddleware(promiseMiddleware, thunk))
    );
    
    export default store;
    ```
    
- reducer
    ```jsx
    //index.js
    **//combineReducers : 각각의 리듀서를 하나로 합쳐준다.
    //https://redux.js.org/api/combinereducers**
    import { combineReducers } from 'redux';
    import userReducer from '../reducers/userReducer';
    import guestReducer from '../reducers/guestReducer';
    import codePostReducer from '../reducers/codePostReducer';
    import adminReducer from '../reducers/adminReducer';
    
    const rootReducer = combineReducers({
      userReducer,
      guestReducer,
      codePostReducer,
      adminReducer
    });
    
    export default rootReducer;
    ```
    
- action
    ```jsx
    // action types
    // user
    export const SIGNIN_USER = 'SIGNIN_USER';
    export const GITHUB_SIGNIN_USER = 'GITHUB_SIGNIN_USER';
    export const KAKAO_SIGNIN_USER = 'KAKAO_SIGNIN_USER';
    export const GOOGLE_SIGNIN_USER = 'GOOGLE_SIGNIN_USER';
    export const SIGNOUT_USER = 'SIGNOUT_USER';
    export const MODIFY_USER_INFO = 'MODIFY_USER_INFO';
    export const DELETE_USER_INFO = 'DELETE_USER_INFO';
    export const MYPAGE_USER_INFO = 'MYPAGE_USER_INFO';
    export const GET_USER_POST_ACTIVE = 'GET_USER_POST_ACTIVE';
    ```
    
    ```jsx
    import {
      SIGNIN_USER,
      GITHUB_SIGNIN_USER,
      KAKAO_SIGNIN_USER,
      GOOGLE_SIGNIN_USER,
      SIGNOUT_USER,
      MODIFY_USER_INFO,
      DELETE_USER_INFO,
      MYPAGE_USER_INFO,
      GET_USER_POST_ACTIVE,
    } from './types';
    import axios from 'axios';
    
    axios.defaults.withCredentials = true;
    const serverUrl = 'https://api.codehigh.club';
    // const serverUrl = 'http://localhost:4000';
    
    //1.로그인(완료)
    export function signinUser(loginInfo) {
      const { email, password } = loginInfo;
    
      const response = axios
        .post(
          `${serverUrl}/auth/email`,
          { email, password },
          {
            headers: { 'Content-Type': 'application/json' },
            withCredentials: true,
            credential: 'include',
          }
        )
        .then((res) => {
          if (res.status === 200) {
            const { id, email, image, name, phone, authorityId, loginType } =
              res.data.userInfo;
            return {
              message: res.data.message,
              accessToken: res.data.accessToken,
              id: id,
              email: email,
              image: image,
              name: name,
              phone: phone,
              authority: authorityId,
              loginType: loginType,
            };
          }
        })
        .catch((err) => {
          if (err.response.status === 401) return 401;
          if (err.response.status === 404) return 404;
        });
    
      return {
        type: SIGNIN_USER,
        payload: response,
      };
    }
    ```
    
- How can I use?
    
    ```jsx
    const userState = useSelector((state) => state.userReducer);
    const { userInfo } = userState;
    ```
    

### redux-saga

[redux-saga](https://www.notion.so/redux-saga-1aaf259d38f640869aeed9909fa4378a)


---
### ref.

- redux 새로고침 상태 유지

[https://developer0809.tistory.com/108](https://developer0809.tistory.com/108)

- redux promise 반환 미들웨어

[https://developer0809.tistory.com/106](https://developer0809.tistory.com/106)

- redux-persist

[https://kyounghwan01.github.io/blog/React/redux/redux-persist/](https://kyounghwan01.github.io/blog/React/redux/redux-persist/)

- redux-saga

[https://redux-saga.js.org/](https://redux-saga.js.org/)