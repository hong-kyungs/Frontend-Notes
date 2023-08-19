# React

## 1. React란?
---

- React는 facebook에서 제공해주는 프론트엔드 라이브러리. → **복잡한 웹/앱에서 data와 화면일치문제를 쉽게 풀어주기 위해 react 사용** - 업데이트 빈도가 높아도 그렇게 무리가 가지 않는데, React는 **가상 DOM**을 사용해 브라우저의 부담을 줄였기 때문입니다. DOM 조작이 브라우저에 엄청 무리를 주기 때문에 가상 DOM을 만들어 달라진 부분만 비교해 업데이트합니다
- 웹페이지에 인터렉션이 자주 발생하고, 동적인 UI를 기존의 JavaScript만으로 표현하면 개발과 수정이 일어날때마다 DOM을 직접 수정해야하기 떄문에 코드가 난잡해지는 문제가 발생하곤 한다.
처리해야 할 이벤트도 다양해지고, 관리해야한 상태 값이나 DOM의 구조도 다양해지게 된다면 이에 따라 처리해야 하는 업데이트 규칙도 복잡해지기 마련이다.

리액트는 이러한 문제점을 개선하기 위해 아래와 같은 방법을 사용한다.

리액트는 **Virtual DOM**이라는 것을 사용한다. 
이 Virtual Dom은 가상의 DOM으로, 브라우저에 실제로 보여지는 DOM이 아니라 단순히 메모리에 가상으로 존재한 DOM으로서, 단순한 JavaScript객체이기 때문에 작동 성능이 브라우저에서 DOM을 보여주는 것보다 속도가 훨씬 빠르다고 한다.
리액트는 상태가 업데이트 되면 업데이트가 필요한 곳의 UI를 가상의 DOM을 통해 렌더링한다. 이때 리액트 내부의 엔진을 통해 실제 브라우저에서 보여지고 있는 DOM과 비교를 한 후, 차이가 있는 곳을 감지해서 실제 DOM에 패치시킨다.

## 2. React의 특징
---

1. Data Flow  
2. Component 기반 구조  
3. Virtual Dom  
4. Props and State  
5. JSX**  

### 1. Data Flow - 단반향 데이터 바인딩

**데이터 바인딩이란?**  
두 데이터 혹은 정보의 소스를 일치시키는 기법으로, 화면에 보이는 데이터(View)와 브라우저 메모리에 있는 데이터(Model, 여러개의 자바스크립트 객체)를 일치시키는 것을 말한다.

예를 들어서 HTML에서 서버 혹은 스크립트상에서 받아온 데이터를 화면상에 그려주고 있다고 가정을 했을 때, 해당 값이 변경이 될 경우 다시 HTML 상에 데이터(값)를 변경된 값에 따라서 맞추어 주는 동작을 '데이터 바인딩'이라고 한다.

**React는 데이터의 흐름이 한 방향으로만 흐르는 단뱡향 데이터 흐름을 가진다.**


<p align="center">
<img src="../../images/react/react_1.png" width="600">
</p>


📌 컴포넌트 내에서 '단방향 데이터 바인딩'은 **Javascript(Model에서 HTML(View)로 한 방향으로만 데이터를 동기화하는 것을 의미**합니다. [JS(Model) -> HTML(View)]

📌 **단방향 데이터 바인딩이기에 역으로 HTML(View)에서 JS(Model)로의 직접적인 데이터 갱신은 불가능**합니다. '이벤트 함수(onClick, onChange,...)'를 주고 함수를 호출한 뒤 Javascript에서 HTML로 데이터를 변경해야 합니다. [HTML(View) -> JS(Model)]

📌 컴포넌트 간에서 단방향 데이터 바인딩은 **부모 컴포넌트에서 자식 컴포넌트로만 데이터가 전달되는 구조입니다.**




참조  
https://narup.tistory.com/183  

(제로초)[https://www.zerocho.com/category/React/post/5774fc91785a21150007807e]  

https://adjh54.tistory.com/49