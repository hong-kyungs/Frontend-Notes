# PureComponent & memo

## React.Component

---

`React.Component`는 [ES6 class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes)를 사용하여 React 컴포넌트를 정의할 때에 기초가 되는 class입니다.

```jsx
class Test extends React.Component {
  state = {
    counter: 0,
  }

  onClick = () => {
    this.setState({})
  }

  render() {
    return (
      <div>
        <button onClick={this.onCLick}>클릭</button>
      </div>
    )
  }
}
```

Test코드에서 버튼을 클릭하면 리렌더링이 될까??
onClick 함수에서 setState하고 있지만 state를 변경한게 없다면 리렌더링이 될까?
**위 예제에서 버튼을 클릭했을때 변하는 state는 없어도 class는 리렌더링이 된다.**

리액트는 Props와 State를 변경하게 되면 보통 리렌더링이 일어난다.
바꾸는 State가 없어도 **SetState 함수를 호출하게되면 리렌더링이 일어나기 때문**이다.

React.Component는 shouldComponentUpdate를 따로 설정해주지 않은 경우, 항상 true를 반환한다.
즉, `setState`가 실행되면 state, props의 변경 여부를 신경쓰지 않고 무조건적으로 컴포넌트를 업데이트시킨다는 것이다.

📍 이때 class는 두가지의 방법으로 리렌더링을 막고 최적화를 할 수 있다.

## React의 라이프사이클 shouldComponentUpdate

---

```jsx
class Test extends React.Component {
  state = {
    counter: 0,
  }

  // 이부분!
  shouldComponentUpdate(nextProps, nextState) {
    if (this.state.counter !== nextStaste.count) {
      return true
    }

    return false
  }

  onClick = () => {
    this.setState({})
  }

  render() {
    return (
      <div>
        <button onClick={this.onCLick}>클릭</button>
      </div>
    )
  }
}
```

리액트의 라이프 사이클인 shouldComponentUpdate를 추가한다.
shouldComponentUpdate 함수는 현재 state와 변경되는 state를 비교하여 리렌더링을 할 것인지를 결정하는데, 위의 코드에서 nextState가 변경되는 state이고 this.state가 현재 state이다.

코드의 반환 값이 true일 경우에 리렌더링이 일어나며 false일 경우에 리렌더링이 일어나지 않는다.
따라서 **리렌더링을 해야 하는 경우를 구체화하는 코드를 추가하여 최적화 할 수 있다.**

## ReactPureComponent

---

pure에는 shouldComponentUpdate가 이미 구현되어 있는데 , props랑 state를 얕은 비교를 통해 비교한 뒤 변경된 것이 있을때는 true를 return 해서 리렌더링 하고, 변경된 것이 없을때는 false를 리턴한다

```jsx
class Test extends PureComponent{
// ...
```

React 컴포넌트의 `render()` 함수가 동일한 props와 state에 대하여 동일한 결과를 렌더링한다면, `React.PureComponent`를 사용하여 경우에 따라 성능 향상을 누릴 수 있습니다.

📍 주의할 점
`React.PureComponent`의 `shouldComponentUpdate()`는 컴포넌트에 대하여 얕은 비교만을 수행합니다. 따라서 컴포넌트에 복잡한 자료 구조가 포함되어있다면, 깊은 차이가 존재함에도 불구하고 차이가 없다고 판단하는 잘못된 결과를 만들어낼 수 있습니다. props와 state의 구조가 간단할 것으로 예상될 때에만 `PureComponent`를 상속하고, 깊은 자료 구조의 변화가 있다면 `[forceUpdate()](https://ko.legacy.reactjs.org/docs/react-component.html#forceupdate)`를 사용해야 한다.

## React.memo

---

`React.memo`는 [고차 컴포넌트(Higher Order Component)](https://ko.legacy.reactjs.org/docs/higher-order-components.html)입니다.

컴포넌트가 동일한 props로 동일한 결과를 렌더링해낸다면, `React.memo`를 호출하고 결과를 메모이징(Memoizing)하도록 래핑하여 경우에 따라 성능 향상을 누릴 수 있습니다. 즉, React는 컴포넌트를 렌더링하지 않고 마지막으로 렌더링된 결과를 재사용합니다.

`React.memo`는 props 변화에만 영향을 줍니다. `React.memo`로 감싸진 함수 컴포넌트 구현에 `useState`, `useReducer` 또는 `useContext` 훅을 사용한다면, 여전히 state나 context가 변할 때 다시 렌더링됩니다.

```jsx
const Try = React.memo(( { props } ) => {
  return (
	 ...
  )
});
```

class에만 PureComponent를 쓸수 있기 때문에, 함수컴포넌트에서는 React.memo를 사용한다.

부모 컴포넌트가 리렌더링됨으로써 자식 컴포넌트가 자동적으로 리렌더링이 되야하는 상황이 있는데, 이럴때 자식컴포넌트에 사용함으로써 부모컴포넌트가 리렌더링 됐을 때 자식컴포넌트가 리렌더링 되는 것을 막아준다. state나 props가 바뀌면 여전히 리렌더링이 잘 된다.

## 정리

pureComponent나 shouldComponentUpdate 그리고 memo는 모두 성능 최적화를 위해 사용한다.

그렇기 때문에 단순히 렌더링을 방지하기 위해 사용하거나 성능적인 이점이 없다면 사용하지 않는것이 좋다.

참조  
[제로초](https://www.youtube.com/watch?v=siiFLSey834&list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&index=35)  
[https://okayoon.tistory.com/entry/React-기초-학습-9-성능최적화-ShouldComponentUpdate-PureComponent-memoMemoizing-Zerocho님-강의-학습-후기](https://okayoon.tistory.com/entry/React-%EA%B8%B0%EC%B4%88-%ED%95%99%EC%8A%B5-9-%EC%84%B1%EB%8A%A5%EC%B5%9C%EC%A0%81%ED%99%94-ShouldComponentUpdate-PureComponent-memoMemoizing-Zerocho%EB%8B%98-%EA%B0%95%EC%9D%98-%ED%95%99%EC%8A%B5-%ED%9B%84%EA%B8%B0)  
[https://velog.io/@dolarge/Pure-Component란](https://velog.io/@dolarge/Pure-Component%EB%9E%80)
