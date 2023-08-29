# useState와 useRef의 차이

## useState와 useRef의 공통점

---

useState와 useRef의 기능상의 공통점은 **함수형 컴포넌트에서 동적으로 상태 관리를 할 수 있게 해준다는 점**이다. 간단한 예시로, 버튼이 클릭 되었을때 주어진 state를 “Humanscape!” 라는 string으로 변환하는 동일한 프로그램을 useState와 useRef를 통해 아래와 같이 다르게 구현할 수 있습니다.

### useState

> `useState` is a React Hook that lets you add a [state variable](https://react.dev/learn/state-a-components-memory) to your component.

```jsx
const Test = () => {
  const [letter, setLetter] = useState('')
  const onClick = () => {
    setLetter('Humanscape!')
  }

  return (
    <div>
      <button onClick={onClick}>Humanscape?</button>
      <b>{letter}</b>
    </div>
  )
}
```

```jsx
const [letter, setLetter] = useState('')
```

`useState` 를 사용 할 때에는 상태의 기본값을 파라미터로 넣어서 호출해준다. 이 함수를 호출해주면 배열이 반환되는데요, 여기서 첫번째 원소는 현재 상태, 두번째 원소는 **Setter 함수**다. **Setter 함수**는 파라미터로 전달 받은 값을 최신 상태로 설정해준다. 즉, setter함수(여기선 setLetter)가 새 state를 받아 컴포넌트 리렌더링 큐에 등록한다.

컴포넌트는 다음 렌더링 시에 `useState`를 통해 반환받은 첫번째 값은 항상 갱신된 최신 state가 된다.

### useRef

> `useRef` is a React Hook that lets you reference a value that’s not needed for rendering.

```jsx
const Test2 = () => {
  const letter = useRef('')

  const onClick = () => {
    letter.current = 'Humanscape!'
    console.log(letter.current)
  }

  return (
    <div>
      <button onClick={onClick}>Humanscape?</button>
    </div>
  )
}
```

`useRef` Hook 은 DOM 을 선택해서 조작하는데 사용되고, 컴포넌트 안에서 조회 및 수정 할 수 있는 변수를 관리하는데 사용된다.

`useRef` 로 관리하는 변수는 값이 바뀐다고 해서 컴포넌트가 리렌더링되지 않습니다. 리액트 컴포넌트에서의 상태는 상태를 바꾸는 함수를 호출하고 나서 그 다음 렌더링 이후로 업데이트 된 상태를 조회 할 수 있는 반면, `useRef` 로 관리하고 있는 변수는 설정 후 바로 조회 할 수 있다

- 포커스, 텍스트 선택영역, 혹은 미디어의 재생을 관리와 같은 DOM을 선택해서 조작하거나, 불필요한 렌더링을 막기위해 값이 바뀌어도 렌더링 시키고 싶지 않은 부분은 useRef에 넣어서 사용한다.

📍

`seState`와 `useRef` 모두 주어진 state를 변화시킬 수 있다는 것을 알아보았다. _useState의 구현에서는 “Humanscape!”라는 글씨를 화면에 띄워서 값이 변한 것을 확인했는데, useRef의 구현에서는 console에 log를 찍어 확인해야한다. 그 이유는?_

## useState와 useRef의 차이점

`useRef`를 사용한 구현에서 글씨를 화면에 띄우지 않은 것은 `useState`와는 다르게 useRef는 state를 변화시킨 후에 component를 re-render하지 않기 때문이다. 다음은 React 공식 문서의 [Hooks API Reference](https://reactjs.org/docs/hooks-reference.html#useref)에 나와있는 내용이다.

_Keep in mind that `useRef` doesn’t notify you when its content changes. **Mutating the `.current` property doesn’t cause a re-render**. If you want to run some code when React attaches or detaches a ref to a DOM node, you may want to use a [callback ref](https://reactjs.org/docs/hooks-faq.html#how-can-i-measure-a-dom-node) instead._

따라서 `useRef`를 사용한 구현에서 state를 변화시키더라도 변화 후에 re-render가 되지 않아 initial value로 나타날 것이기 때문에 rendering을 할 수는 있지만 변화했다는 의미가 존재하지 않아 따로 화면에 띄우지 않은 것입니다.

반면, `useState`의 경우 선언한 state가 setter function에 의해 update될 경우, re-rendering process가 진행됩니다. 다음은 React 공식 문서의 [Hooks API Reference](https://reactjs.org/docs/hooks-reference.html#useref)에 나와있는 내용입니다.

\*The `setState` function is used to update the state. **It accepts a new state value and enqueues a re-render of the component.\***

결과적으로 각각의 **state에서 이용할 hook을 설계할 때, 주로 state의 rendering 여부를 바탕으로 결정하는 것이 좋다.** Rendering이 필요한 state의 경우 `useState`를 이용하는 것이 간편하게 상태관리를 할 수 있으며, rendering이 필요하지 않은 state의 경우 `useRef`를 쓰는 것이 간단하게 코드를 작성하실 수 있습니다.

참조  
[벨로퍼트와 함께하는 모던 리액트](https://react.vlpt.us/basic/12-variable-with-useRef.html)  
https://velog.io/@hyunjine/useState-vs-useRef  
https://medium.com/humanscape-tech/react-usestate-vs-useref-4c20713f7ef
