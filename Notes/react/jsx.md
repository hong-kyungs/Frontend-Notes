# JSX

## JSX란?
---

- JSX는 자바스크립트 확장 문법이다. XML과 매우 비슷하게 생겼으며, 이런 형식으로 작성한 코드는 브라우저에서 실행되기 전에 코드가 번들링되는 과정에서 바벨을 사용해 일반 자바스크립트 형태의 코드로 변환된다.
- 원시적인 형태의 코드는 가독성이 떨어지고 불편해서 React가 JSX문법으로 바꾸었다. (바벨이 JSX → 원시적인 형태로 변화한다.)

```jsx
function App(){
	return (
    	<div>
        	Hello <b>react</b>
        </div>
    );
}
```

위의 코드는 아래와 같이 변환된다.

```jsx
function App(){
	return React.createElement("div", null, "Hello", React.createElement("b", null "react"));
}
```

- 만약 컴포넌트를 렌더링 할 때 마다 위 코드처럼 매번 React.createElement 함수를 사용해야 한다면 매우 불편할 것이다. JSX를 사용하면 편하게 UI를 렌더링 할 수 있다.

## JSX 문법 규칙
---

### 1. 꼭 닫혀야 하는 태그

태그는 꼭 닫혀있어야 한다.

```jsx
function App(){
    return(
    	<div>
        	<h1>테스트1</h1>
        	<h2>테스트2</h2>
        </div>
    )
}
```

### 2. 꼭 감싸져야 하는 태그

두개 이상의 태그는 무조건 하나의 태그로 감싸져있어야 한다.

```jsx
function App(){
    return(
    	<>
        	<h1>테스트1</h1>
        	<h2>테스트2</h2>
       <>
    )
}
```

이렇게 감싸는 이유는, 리액트가 사용하는 Virtual DOM 방식에서는 컴포넌트 변화를 감지할 때 효율적으로 비교하고자 컴포넌트 내부는 하나의 DOM 트리 구조로 이루어져야 한다는 규칙이 있기 때문이다.

### 3. JSX 안에 자바스크립트 값 사용하기

JSX 내부에 자바스크립트 변수를 보여줘야 할 때에는 `{}` 으로 감싸서 보여준다.

```jsx
function App() {
  const name = 'react';
  return (
    <>
      <Hello />
      <div>{name}</div>
    </>
  );
}
```

### 4. 조건부 렌더링

- **삼항 연산자(조건부 연산자)를 사용한 조건부 렌더링**
    
    JSX 내부의 JS 표현식에서는 if문을 사용할 수 없다. 때문에 조건에 따라 다른 내용을 렌더링 하고자 할 경우 JSX 밖에서 if 문을 사용하거나, 중괄호 안에서 삼항 연산자를 사용하면 된다.
    

```jsx
class App extends Component {
    render() {
        let name = 'React';
        return (
            <div>
                {
                    name === 'React' ? (
                        <h1>This is React.</h1>
                    ) : (
                        <h1>This is not React.</h1>
                    )
                }
            </div>
        );
    } 
}
```

- AND 연산자(&&)를 사용한 조건부 렌더링
    
    특정 조건을 만족할 때만 내용을 보여주고 싶을 때 사용
    

```jsx
class App extends Component {
    render() {
        let name = 'React';
        return (
            <div>
                {
                    name === 'React' && <h1>This is React.</h1>
                }
            </div>
        );
    } 
}
```

### 5. undefined를 렌더링하지 않기

리앤트 컴포넌에서는 함수에서 undefinead만 반환하여 렌더링하는 상황을 만들면 안 된다. 예를 들어 다음과 같은 코드는 오류를 발생시킨다.

```jsx
import React from 'react';
import './App.css';

// undefined를 렌더링 하지 않기
function App(){
	const name = 'undefined';
	return name;
}

export default App;
```

어떤 값이 undefined일 수도 있다면, OR( || )연산자를 사용하면 해당 값이 undefined일 때 사용할 값을 지정할 수 있으므로 간단하게 오류를 방지할 수 있다.

```jsx
import React from 'react';
import './App.css';

function App(){
	const name = 'undefined';
	return name || '값이 undefined입니다.';
}

export default App;
```

반면 JSX 내부에서 undefined를 렌더링하는 것은 괜찮다.

```jsx
import React from 'react';
import './App.css';

function App(){
	const name = 'undefined';
	return <div>{name}</div>
}

export default App;
```

name 값이 undefined일 떄 보여 주고 싶은 문구가 있다면 다음과 같이 코드를 작성할 수 있다.

```jsx
import React from 'react';
import './App.css';

function App(){
	const name = 'undefined';
	return <div>{name || 'react'}</div>;
}

export default App;
```

### 6. style 과 className

JSX 에서 태그에 `style` 과 CSS class 를 설정하는 방법은 HTML 에서 설정하는 방법과 다르다.

우선, 인라인 스타일은 객체 형태로 작성을 해야 하며, `background-color` 처럼 `-` 로 구분되어 있는 이름들은 `backgroundColor` 처럼 camelCase 형태로 네이밍 해주어야 한다.

```jsx
function App() {
  const style = {
      backgroundColor: 'white',
      fontSize: '10px',
      fontWeight: 'bold'
  }
  return (
  	<div style={style}>테스트</div>
  )
```

그리고, CSS class 를 설정 할 때에는 `class=` 가 아닌 `className=` 으로 설정을 해주어야 한다.

```jsx
<div className="classEx1"></div>
```

### 7. 반복문(map)

JSX 내부에선 for구문을 이용할 수 없다. 반복문을 처리해야 한다는 map 이용해야 한다.

```jsx
const iterationSample = () => {
  const fruit = ["사과", "포도", "딸기", "수박"];
  const fruitList = names.map((name) => <li>{name}</li>);

  return <ul>{nameList}</ul>;
};
```

참조  
제로초  
https://react.vlpt.us/basic/04-jsx.html  
https://developerntraveler.tistory.com/54     
[https://velog.io/@gyumin_2/React-JSX란정의-장점-문법-특징-등](https://velog.io/@gyumin_2/React-JSX%EB%9E%80%EC%A0%95%EC%9D%98-%EC%9E%A5%EC%A0%90-%EB%AC%B8%EB%B2%95-%ED%8A%B9%EC%A7%95-%EB%93%B1)  