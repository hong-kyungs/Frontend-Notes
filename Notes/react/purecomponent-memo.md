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

참조
[제로초](https://www.youtube.com/watch?v=siiFLSey834&list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&index=35)  
[https://okayoon.tistory.com/entry/React-기초-학습-9-성능최적화-ShouldComponentUpdate-PureComponent-memoMemoizing-Zerocho님-강의-학습-후기](https://okayoon.tistory.com/entry/React-%EA%B8%B0%EC%B4%88-%ED%95%99%EC%8A%B5-9-%EC%84%B1%EB%8A%A5%EC%B5%9C%EC%A0%81%ED%99%94-ShouldComponentUpdate-PureComponent-memoMemoizing-Zerocho%EB%8B%98-%EA%B0%95%EC%9D%98-%ED%95%99%EC%8A%B5-%ED%9B%84%EA%B8%B0).  
[https://velog.io/@dolarge/Pure-Component란](https://velog.io/@dolarge/Pure-Component%EB%9E%80)
