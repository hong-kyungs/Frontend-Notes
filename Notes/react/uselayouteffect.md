# useEffect와 useLayoutEffect의 차이

<p align="center">
<img src="../../images/react/react-hook-flow.png" width="400">
</p>

- **Render:** DOM Tree 를 구성하기 위해 각 엘리먼트의 스타일 속성을 계산하는 과정
- **Paint:** 실제 스크린에 Layout을 표시하고 업데이트하는 과정

## useEffect

useEffect 는 컴포넌트들이 render 와 paint 된 후 실행된다. **비동기적(asynchronous)** 으로 실행된다. paint 된 후 실행되기 때문에, useEffect 내부에 dom 에 영향을 주는 코드가 있을 경우 사용자 입장에서는 **화면의 깜빡임과 동시에 화면 내용이 달라진다.**

## useLayoutEffect

useLayoutEffect 는 컴포넌트들이 render 된 후 실행되며, 그 이후에 paint 가 된다. 이 작업은 **동기적(synchronous)** 으로 실행된다. paint 가 되기전에 실행되기 때문에 dom 을 조작하는 코드가 존재하더라도 사용자는 **깜빡임을 경험하지 않는다. useEffect와 기능은 동일하되 실행 시점만 다르다.**

## 정리

기본적으로 useEffect를 사용하고, state update 떄문에 화면에 깜밖임이 발생하거나 간만에 차이로 리렌더링이 발생하는 것 같을 때, useLayoutEffect를 써서 react hook flow에서 실행순서를 조금 앞당긴다.

참조  
[https://medium.com/@jnso5072/react-useeffect-와-uselayouteffect-의-차이는-무엇일까-e1a13adf1cd5](https://medium.com/@jnso5072/react-useeffect-%EC%99%80-uselayouteffect-%EC%9D%98-%EC%B0%A8%EC%9D%B4%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C-e1a13adf1cd5)
