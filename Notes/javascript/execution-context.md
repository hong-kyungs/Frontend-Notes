# 실행 컨텍스트(execution context)

## 실행 컨텍스트

실행 컨텍스트(Execution Context)는 scope, hoisting, this, function, closure 등의 동작원리를 담고 있는 자바스크립트 핵심원리이다.

실행 컨텍스트를 바로 이해하지 못하면 코드 독해가 어려워지며 디버깅도 매우 곤란해 질 것이다.

자바스크립트 엔진은 코드를 실행하기 위해서 실행에 필요한 여러가지 정보를 알고 있어야 한다.

실행에 필요한 여러가지 정보란 아래와 같은 것들이 있다.

- 변수 : 전역변수, 지역변수, 매개변수, 객체의 프로퍼티
- 함수 선언
- 변수의 유효범위(Scope)
- this

이와 같이 실행에 필요한 정보를 형상화하고 구분하기 위해 자바스크립트 엔진은 실행 컨텍스트를 물리적 객체의 형태로 관리한다.

```jsx
var x = 'xxx'

function foo() {
  var y = 'yyy'

  function bar() {
    var z = 'zzz'
    console.log(x + y + z)
  }
  bar()
}
foo()
```

위 코드를 실행하면 아래와 같이 실행 컨텍스트 스택(stack)이 생성하고 소멸한다.

현재 실행 중인 컨텍스트에서 이 컨텍스트와 관련없는 코드(예를 들어 다른 함수)가 실행되면 새로운 컨텍스트가 생성된다.

이 컨센스트는 스택에 쌓이게 되고 컨트롤(제어권)이 이동한다.

<p align="center">
<img src="../../images/javascript/execution-context-1.png width="600">
</p>

⇒ 실행 컨텍스트는 자바스크립트 코드가 실행되는 환경이다. 모든 JS코드는 실행 컨텍스트 내부에서 실행된다고 생각하면 된다. 즉 함수가 실행되면 함수 실행에 해당하는 실행 컨텍스트가 생성되고, 자바스크립트 엔진에 있는 콜 스택에 차곡차곡 쌓인다.

## 실행 컨텍스트의 3가지 객체

참조

[https://inpa.tistory.com/entry/JS-📚-실행-컨텍스트#실행\_컨텍스트](https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EC%8B%A4%ED%96%89-%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8#%EC%8B%A4%ED%96%89_%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8)

https://velog.io/@edie_ko/js-execution-context
