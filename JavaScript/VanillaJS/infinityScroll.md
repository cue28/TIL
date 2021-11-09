# 무한 스크롤

```jsx
//!새로고침 시, 스크롤 상단
  window.onload = function(){
    setTimeout(()=> {
      scrollTo(0,0);
    },100)
  }
```

```jsx
import React, { useEffect, useState } from 'react';
import { getReviewPost } from '../../redux/actions/codePostActions';
import { resetCodereviewPost } from '../../redux/actions/codePostActions';
import { useSelector, useDispatch } from 'react-redux';
import SearchInput from '../basic/search/SearchInput';

function CodeReviewBoard() {
  const [count, setCount] = useState(2);
  const state = useSelector((state) => state.codePostReducer);
  const { postList } = state;
  const dispatch = useDispatch();

  //!새로고침 시, 스크롤 상단
  window.onload = function () {
    setTimeout(() => {
      scrollTo(0, 0);
    }, 100);
  };

  //!새로고침하면 첫 15개만 나타남
  useEffect(() => {
    dispatch(resetCodereviewPost());
  }, []);
  console.log('코드리뷰보드에서의 코드리스트', postList);

  const getMorePost = async () => {
    try {
      dispatch(getReviewPost(count));
      setCount(count + 1);
    } catch (err) {
      console.log(err);
    }
    // if (addList.length !== 0 && addList.length <= 6) {
    //   const addContent = document.createElement('div');
    //   addContent.classList.add('codereviewboard-card');
    //   addContent.innerHTML = `{addList.map((item) => {
    //         return (<h1>item.title</h1>
    //             <div>item.codeContent</div>);
    //     })}`;
    //   document.querySelector('section').appendChild(addContent);
    // } else {
    //   return;
    // }
  };
  console.log(count);
  const onScroll = async (e) => {
    try {
      const { clientHeight, scrollTop, scrollHeight } = e.target.scrollingElement;
      if(clientHeight + scrollTop === scrollHeight) {
        getMorePost();
      }
    } catch (err) {
      console.log(err);
    }
    //window.innerHeight=1006 , window.scrollY=1, document.body.offsetHeight=1007
    // console.log(document.querySelector('section').scrollTop);
    // console.log(e.target.scrollingElement.scrollTop);
    // console.log(window.innerHeight, window.scrollY, document.body.offsetHeight);
    // if (scrollTop + clientHeight === scrollHeight) {
    //   getMorePost()
    //   console.log('onScroll 여기서 반복')
    // }
  };

  document.addEventListener('scroll', onScroll);
  // document.removeEventListener('scroll', onScroll);

  return (
    <div className='codereviewboard'>
      <div className='codereviewboard-container'>
        <div className='codereviewboard-header'>
          <SearchInput />
        </div>
        <section className='codereviewboard-cardbox'>
          {postList.map((item, index) => {
            return (
              <div className='codereviewboard-card' key={index}>
                <h1>{item.title}</h1>
                <div>{item.codeContent}</div>
              </div>
            );
          })}
          {/* <div className='codereviewboard-loding'>로딩중</div> */}
        </section>
      </div>
    </div>
  );
}

export default CodeReviewBoard;
```

ref.

[https://www.youtube.com/watch?v=hVcriryAVbg](https://www.youtube.com/watch?v=hVcriryAVbg)

[https://github.com/fc-secret-code/Secretcode_InfiniteScroll](https://github.com/fc-secret-code/Secretcode_InfiniteScroll)