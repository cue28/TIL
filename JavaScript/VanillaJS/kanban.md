# 칸반보드

### 칸반보드란?
- 개인적으로나 회사에서 작업, 일정을 관리하기 위래 사용한 도구들 중 하나
- 작업 항목에 대한 카드를 사용해 각 프로세스 단계를 칼럼을 통해 시각적으로 표현
- 진행 상황을 한 눈에 파악할 수 있고, 작업 관리에 효율적

### 사용 이유
- 파이널 프로젝트 주제로 코드를 저장하고, 이해도에 따른 분류를 사용자가 보다 편리하고 직관적으로 할 수 있게 하기 위함.
- 무한 스크롤은 첫 로딩 시 데이터를 받아오는 시간을 최소화해주고, 페이지네이션에 직접 페이지를 클릭해야한다는 수고스러움을 덜어주기 위함.

### 드래그 앤 드롭 마우스 이벤트 - 문서 복사 이동, 장바구니 물건 놓기 등

대상에 대한 이벤트
- dragstart, 드래그가 시작했을 때 발생
- dragend, 드래그가 끝났을 때 발생 → 고유동작중단,

- dragover, 블록을 적합한 대상 위로 지나갈 때 발생 → 고유동작중단, 진하게
- dragenter, 적합한 대상 위로 올라갔을 때 발생 → 대상 색상 진하게
- dragleave, 드롭 대상에서 벗어 났을 때 발생 → 원래 색상으로
- drop 대상에 드롭했을 때 → 원래 색상으로
- 이벤트를 사용

블록에 대한 이벤트
- 3가지 종류의 칸을 만듬, 옮겨다닐 카드와, 칸을 DOM querySelectorAll로 배열에 담아줌
- 선택한 카드에 dragstart가 시작되면 화면영역에서 사라지게 만듬
- dragend로 드래그가 끝나면 다시 보이게 만들어줌

option
- e.preventDefault() → 고유 동작을 중단시킴
- 칸에는 draggable='true' → 드래그 가능한 속성으로 만들기



```jsx

function Kanban() {
  //Redux 사용 후 상태 유지, 데이터 전송 관리하기
  let mockCode = [
    {'subject':'알고리즘1', 'date':'2021.09.14', 'code':'if(now === night){return `I have to go to bed.`}'},
    {'subject':'알고리즘2', 'date':'2021.09.14', 'code':'if(now === night){return `I have to go to bed.`}'},
    {'subject':'알고리즘3', 'date':'2021.09.14', 'code':'if(now === lunch){return `I wanna sleep`}'},
    {'subject':'알고리즘4', 'date':'2021.09.14', 'code':'if(now === night){return `I have to go to bed.`}'},
    {'subject':'알고리즘5', 'date':'2021.09.14', 'code':'if(now === morning){return `OMG`}'},
    {'subject':'알고리즘6', 'date':'2021.09.14', 'code':'if(now === night){return `I have to go to bed.`}'},
    {'subject':'알고리즘7', 'date':'2021.09.14', 'code':'if(now === richguy){return `I will run.!`}'},
    {'subject':'알고리즘8', 'date':'2021.09.14', 'code':'if(now === night){return `I have to go to bed.`}'},
  ]

  useEffect(() => {
    const list_items = document.querySelectorAll('.kanban-list-item');
    const lists = document.querySelectorAll('.kanban-list');
    console.log('list', list_items); //!빈객체임

    let draggedItem = null;

    for (let i = 0; i < list_items.length; i++) {
      const item = list_items[i];

      item.addEventListener('dragstart', function () {
        draggedItem = item;
        setTimeout(() => {
          item.style.display = 'none';
        }, 0);
      });

      item.addEventListener('dragend', function () {
        setTimeout(() => {
          draggedItem.style.display = 'block';
          draggedItem = null;
        }, 0);
      });

      for (let j = 0; j < lists.length; j++) {
        const list = lists[j];

        list.addEventListener('dragover', function (e) {
          e.preventDefault();
        });
        list.addEventListener('dragenter', function (e) {
          e.preventDefault();
          list.style.backgroundColor = 'rgba(0, 0, 0, 0.2)';
        });
        list.addEventListener('dragleave', function(e){
          list.style.backgroundColor = 'rgba(0, 0, 0, 0.1)';
        })
        list.addEventListener('drop', function (e) {
          console.log('drop');
          list.append(draggedItem);
          list.style.backgroundColor = 'rgba(0, 0, 0, 0.1)';
        });
      }
    }
  }, []);

  return (
    <div className='kanban'>
      <div className='kanban-container'>
        {/* 헤더 */}
        <div className='kanban-header'>
          <SearchInput />
          <Button content='NEW' backgroundColor='#2F8C4C' color='#fff'/>
        </div>
        <div className='kanban-subject'>
          <div>이해도 (하)</div>
          <div>이해도 (중)</div>
          <div>이해도 (상)</div>
        </div>
        <div className='kanban-list-container'>
          <section className='kanban-list'>
            {mockCode.map((item) => {
              return <div className='kanban-list-item' draggable='true'>
              <h1>[ {item.subject} ]</h1>
              <div>{item.date}</div>
              <div>{item.code}</div>
            </div>
            })}
          </section>
          <section className='kanban-list'></section>
          <section className='kanban-list'></section>
        </div>
        {/* 푸터 */}
      </div>
    </div>
  );
}
```

```scss
.kanban {
  display: flex;
  align-items: center;
  justify-content: center;
}

.kanban-container{
  width: 1200px;
  display: flex;
  flex-direction: column;
}

.kanban-header{
  display: flex;
  justify-content: space-between;
  margin: 10px;
    span:nth-child(2){
      padding: 0px 40px;
    }
}

.kanban-subject{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  margin-top: 10px;
    div{
      font-size: 1.5rem;
      font-weight: 600;
      margin-left: 15px;
      color: #{$green};
    }
}

.kanban-list-container{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}

.kanban-list {
  background-color: #{$gray};
  height: 80vh;
  padding: 10px;
  margin: 10px;
  overflow-y: scroll;
}

.kanban-list-item {
  background-color: white;
  font-size: 2.0rem;
  margin: 10px 0;
  font-family: 'Nanum Gothic';
  height: 130px;
  padding: 10px;
  cursor:grab;
   &:active {
     cursor:grabbing;
   }
   h1{
     font-size: 1.5rem;
     margin-bottom: 5px;
   }
   div:nth-child(2){
     font-size: 1.3rem;
     margin-bottom: 10px;
   }
   div:nth-child(3){
    font-size: 1.5rem;
  }
}

.kanban-list .kanban-list-item {
  transition: all 0.2s linear;
}
```

ref.
[https://developer.mozilla.org/ko/docs/Web/API/HTML_Drag_and_Drop_API](https://developer.mozilla.org/ko/docs/Web/API/HTML_Drag_and_Drop_API)

[https://www.youtube.com/watch?v=tZ45HZAkbLc](https://www.youtube.com/watch?v=tZ45HZAkbLc)

