# Context API

## Context 란?

Context는 리액트 컴포넌트간에 어떠한 값을 공유할수 있게 해주는 기능이다. 주로 Context는 전역적(global)으로 필요한 값을 다룰 때 사용하는데, 꼭 전역적일 필요는 없다. Context를 단순히 "리액트 컴포넌트에서 Props가 아닌 또 다른 방식으로 컴포넌트간에 값을 전달하는 방법이다" 라고 접근을 하는 것이 좋다.

## Context 사용하는 이유?

기존에 컴포넌트 간에 데이터를 전달하려면 props를 이용해야 했다. props는 부모 자식 관계에서 데이터를 전달한다. 따라서 A, B, C 컴포넌트가 각각 부모자식 관계일 때, A에서 C로 데이터를 내려보내주려면 중간 B 컴포넌트를 거쳐야 했다.. A, B, C, D, E 컴포넌트일 때 A에서 E로 데이터를 내려보내주려면 중간 B, C, D 컴포넌트를 거쳐야 하기에 엄청나게 비효율적이다. - 이러한 복잡한 구조를 해결하기 위해 context API가 나왔다.

## Context 사용법

### 1. createContext

Context 는 리액트 패키지에서 `createContext` 라는 함수를 불러와서 만들 수 있다.

```jsx
import React, { createContext } from 'react'
```

Context 객체 안에는 Provider라는 컴포넌트가 들어있습니다. 그리고, 그 컴포넌트간에 공유하고자 하는 값을 `value` 라는 Props로 설정하면 자식 컴포넌트들에서 해당 값에 바로 접근을 할 수 있습니다.

createContext 내부에 공유하길 원하는 데이터의 초깃값을 넣어두고 value 변수로 묶어주면 된다. 이 때 value 객체는 객체이므로 리렌더링의 주범이 되므로 useMemo로 캐싱해둔다. 안 그러면 나중에 이 데이터를 쓰는 모든 컴포넌트가 매번 리렌더링된다.

```jsx
import React, { createContext, useMemo, useState } from 'react'
import Parent from './Parent'

export const UserContext = createContext({
  setLoggedIn: () => {},
  setLoading: () => {},
})
const GrandParent = () => {
  const [loggedIn, setLoggedIn] = useState(false)
  const [loading, setLoading] = useState(false)
  const value = useMemo(() => ({ setLoggedIn, setLoading }), [
    setLoggedIn,
    setLoading,
  ])
  return (
    <UserContext.Provider value={value}>
      <Parent />
      <div>{loggedIn ? '로그인' : '로그인안해'}</div>
      <div>{loading ? '로딩중' : '로딩안해'}</div>
    </UserContext.Provider>
  )
}
export default GrandParent
```

### 2. useContext

현재 컴포넌트 구조는 GrandParent - Parent - Children이다. GrandParent에서 선언한 setLoggedIn과 setLoading을 Parent를 거치지 않고 바로 Children으로 보낼 것이다. 그러기 위해서는 컴포넌트가 UserContext.Provider로 감싸져있어야 합니다. value props에 아까 만든 value를 넣어둔다.

Parent는 아무 것도 안한다. 과연 Children은 GrandParent의 컨텍스트를 물려받을 수 있을까?

```jsx
import React from 'react'
import Children from './Children'

const Parent = () => {
  return <Children />
}
export default Parent
```

원하는 컴포넌트에서 `useContext` 라는 Hook을 사용하여 Context에 넣은 값에 바로 접근할 수 있습니다. 해당 Hook의 인자에는 `createContext`로 만든 `Usercontext` 를 넣습니다. `useContext`를 불러와서 안에 `UserContext`를 넣어주면 `setLoading`과 `setLoggedIn`을 쓸 수 있다.

```jsx
import React, { useContext } from 'react'
import { UserContext } from './GrandParent'

const Children = () => {
  const { setLoading, setLoggedIn } = useContext(UserContext)
  return (
    <>
      <button onClick={() => setLoading((prev) => !prev)}>로딩토글</button>
      <button onClick={() => setLoggedIn((prev) => !prev)}>로딩토글</button>
    </>
  )
}
export default Children
```

## Context API의 문제점? 주의할 점?

우선 Context API를 이야기하면 가장 먼저 나오는 문제인 **렌더링 이슈**다.

**Provider에 제공한 value가 달라지면 useContext를 쓰고 있는 모든 컴포넌트가 리렌더링 된다는 것**이다. Provider 컴포넌트는 매번 Provider에 새로운 값이 지정되어 있는지 확인하고, 값이 새로운 참조일 경우에 리렌더링이 발생하게 되고 해당 컨텍스트를 둘러싸고 있는 모든 컴포넌트가 리렌더링된다.

value 안에는 setLoading과 setLoggedIn이 들어있고 앞으로 개수가 더 늘어날 가능성이 높다. 그 중 하나라도 바뀌면 객체로 묶여있으므로 전체가 리렌더링되는 것이다. 따라서 잘못 쓰면 엄청난 렉을 유발할 수 있다. 해결 방법은 자주 바뀌는 것들을 별도의 컨텍스트로 묶거나(컨텍스트는 여러 개 쓸 수 있다. Provider로만 잘 감싸야한다.), 자식 컴포넌트들을 적절히 분리해서 shouldComponentUpdate, PureComponent, React.memo 등으로 감싸주는 것이 있습니다.

## Redux랑 차이는 무엇인가?

과거에는 리액트의 Context가 굉장히 불편해서 전역 상태 관리 라이브러리를 사용하는 것이 당연시 여겨졌던 시절이 있었지만 이제는 사용하기 편해져서 단순히 전역적인 상태를 관리하기 위함이라면 더 이상 사용해야 할 이유가 없다.

단, "상태 관리 라이브러리"와 Context는 완전히 별개의 개념임을 잘 이해하셔야 합니다. Context는 전역 상태 관리를 할 수 있는 수단일 뿐이고, 상태 관리 라이브러리는 상태 관리를 더욱 편하고, 효율적으로 할 수 있게 해주는 기능들을 제공해주는 도구이다.

Context Provider value에 React.useState의 반환 값을 넣어주고, 사용하는 측에서 **setState를 직접** 관리해주었어야 한다. 즉, Context API가 상태 관리를 해주는 것이 아닌 실질적인 상태 관리는 useState와 useReducer로 동작하게 되는 것이다.

Redux의 경우에는 액션과 리듀서라는 개념을 사용하여 상태 업데이트 로직을 컴포넌트 밖으로 분리 할 수 있게 해주며, 상태가 업데이트 될 때 실제로 의존하는 값이 바뀔 때만 컴포넌트가 리렌더링 되도록 최적화를 해줍니다. 만약 Context를 쓴다면, 각기 다른 상태마다 새롭게 Context를 만들어주어야 하는데, 이 과정을 생략할 수 있기에 편리하다. - **Redux는 상태 관리 + 리렌더링 최적화**

참조  
[제로초](https://www.zerocho.com/category/React/post/5fa63fc6301d080004c4e32b)  
https://velog.io/@velopert/react-context-tutorial  
[https://hong-jh.tistory.com/entry/Context-API는-왜-쓰고-그렇다면-Redux는-필요없을까](https://hong-jh.tistory.com/entry/Context-API%EB%8A%94-%EC%99%9C-%EC%93%B0%EA%B3%A0-%EA%B7%B8%EB%A0%87%EB%8B%A4%EB%A9%B4-Redux%EB%8A%94-%ED%95%84%EC%9A%94%EC%97%86%EC%9D%84%EA%B9%8C)
