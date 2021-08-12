# Redux
## Redux란?
기존의 복잡한 MVC 구조에서 단일 store를 생성해 하나의 플로우로 앱이 동작되게 한다.
## 주요 개념
### action
앱의 저장소로 data를 내보낸다. action이 호출되면 state를 변경한다. action의 경우 type을 설정해야 하며 type은 보통 문자열로 정의된다.   
```
export function selectBook(book){    
  return {     
    type: 'BOOK_SELECT',   
    payload: book   
  };   
}   
```
### reducer
action의 type에 따라 새롭게 변화는 state를 반환한다.
```
//initialState는 초기 데이터
function reducer(state = initialState, action){
  switch(action.type){
    case 'BOOK_SELECT':
      return{
        books: state.books,
        selected: action.payload
      }
    default:
      return state;
  }
}

export default reducer;
```

### store
action과 reducer를 저장하는 단 하나의 저장소다.
```
import { Provider } from 'react-redux';
import { createStore } from 'redux'
import reducer from './reducer.js';

const store = createStore(reducer);

ReactDOM.render(
  <Provider store={store}>
    <React.StrictMode>
      <App />
    </React.StrictMode>
  </Provider>,
  document.getElementById('root')
);
```


## 예제
BookList 하나를 클릭했을 시, 선택된 책의 상세 정보를 BookDetail에 나타내고 싶다면?   
onClick함수를 이용해 설정된 type으로 action을 내보내면 reducer는 지정된 action의 type에 따라 state가 바뀌고 영향을 받는 state가 BookDetail에 나타나게 된다.
```
function BookList({books, dispatch}){
  return(
    <List component="nav" aria-label="main list">
      {books.map(item => (
        <div key={item.title}>
          <ListItem button onClick={() => {
            // alert(item.title);
            console.log(item);
            console.log(dispatch);
            //디스패치 시켜서 액션을 내보내면 그 액션이  리듀서를 타고 돌아서 스테이트 바뀌게 되고 바뀐 스테이트에 영향을 받는 애들만 새로 그려진다.
            dispatch({ type: 'BOOK_SELECT', payload: item});
          }}>
            <ListItemText
              primary={item.title}
              secondary={item.subtitle}
            />      
            <Badge badgeContent={item.likes} color="secondary">
              <FavoriteIcon style={{color: 'pink'}} />
            </Badge>    
          </ListItem>
          <Divider/>
        </div>
      ))}
    </List>
  );
};
```

