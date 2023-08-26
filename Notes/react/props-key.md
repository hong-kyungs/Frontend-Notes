# props에 key를 사용하는 이유

## What is key in React?

---

> Key는 React가 어떤 항목을 변경, 추가 또는 삭제할지 식별하는 것을 돕습니다. key는 엘리먼트에 안정적인 고유성을 부여하기 위해 배열 내부의 엘리먼트에 지정해야 합니다. - 리액트 공식문서

## \***\*key엔 어떤 값을 써야할까?\*\***

---

Key 값은 list에서 해당 항목을 고유하게 식별할 수 있는 문자열이 가장 좋다.
대부분의 경우 **데이터의 ID**를 key로 사용한다.

📍 **주의 : 배열의 index를 사용하는 건 지양하자**

key값을 배열의 index로 지정할 경우, 배열의 순서가 바뀌면 component의 state와 관련된 문제가 발생할 수 있다. component는 key를 기반으로 갱신/재사용되는데 index를 key로 사용하면, 항목의 순서가 바뀌었을 때 key도 변경된다. 따라서 state까지 의도치않게 변경될 수 있다.

명시적으로 key를 지정하지 않을 경우 React는 기본적으로 인덱스를 key로 사용하니, 가급적이면 별도로 key값을 지정하자.

## \***\*map함수 적용시 Key props를 사용하는 이유는?\*\***

---

아래와 같이 key값이 없는 element로 이루어진 트리에서 새로운 element가 추가될 경우, React는 `<ul>`의 모든 자식요소를 다시 변경하므로 비효율적이고 성능이 좋지 않다.

```jsx
class TodoList extends Component {
  render() {
    const todos = [
      { id: 1, text: '청소' },
      { id: 2, text: '독서' },
      { id: 3, text: '운동' },
    ]
    const todoItems = todos.map((todo) => <li>{todo.text}</li>)
    return <ul>{todoItems}</ul>
  }
}
```

**key를 이용하면 앞서 말한 비효율성을 해결할 수 있다.**

자식요소들이 key를 가지고 있다면, React는 key를 통해 기존 트리와 이후 트리의 자식들이 일치하는지 확인하므로 트리의 변환이 효율적으로 이루어진다.

### 설정

key값은 map한수의 인자로 전달되는 함수 내부에서 컴포넌트 props를 설정하듯이 설정하면 된다

```jsx
class TodoList extends Component {
  render() {
    const todos = [
      { id: 1, text: '청소' },
      { id: 2, text: '독서' },
      { id: 3, text: '운동' },
    ]
    const todoItems = todos.map((todo) => <li key={todo.id}>{todo.text}</li>)
    return <ul>{todoItems}</ul>
  }
}
```

## 정리

---

리액트는 반복문안에서 동적으로 만들어지는 태그는 고유의 key 값을 부여해야 하는데, 이는 리액트가 key 값을 통해서 동적 태그를 추적해 리액트가 성능을 높이고 정확한 동작을 하게 한다.

참조  
리액트 - 공식문서  
https://dev-bomdong.tistory.com/m/12  
https://foxtrotin.tistory.com/219
