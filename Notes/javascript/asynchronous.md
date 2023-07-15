# 비동기처리(Asynchronous) - callback, promise, async, await

## 자바스크립트의 동기와 비동기

자바스크립트는 **싱글 스레드 언어**이기 때문에 한 번에 하나의 작업만 수행할 수 있다. 즉, 이전 작업이 완료되어야 다음 작업을 수행할 수 있게 된다. 우리가 프로그래밍을 하면서 일반적으로 각 함수와 코드들이 위에서 아래로 차례로 동작하는 방식이라고 할 수 있다. 이러한 코드 순차 실행을 **동기(Synchronous)** 라고 부른다.

그런데 동기 방식은 간단하고 직관적이지만, 작업이 오래 걸리거나 응답이 늦어지는 경우에는 전체적인 성능과 사용자 경험에 영향을 줄 수 있다. 예를 들어 서버에 데이터를 요청하고 응답을 받아야 하는 작업이 있다면, 응답이 올 때까지 다른 작업을 하지 못하고 대기해야 한다. 이렇게 되면 프로그램의 흐름이 멈추거나 지연되게 된다.

<p align="center">
<img src="../../images/javascript/asynchronous-1.png" width="600">
</p>

따라서 자바스크립트로 여러 작업을 동시에 처리하기 위해 **비동기(Asynchronous)** 라는 개념을 도입하여, 특정 작업의 완료를 기다리지 않고 다른 작업을 동시에 수행할 수 있도록 하였다. 자바스크립트를 배우다 보면 setTimeout() 함수나 fetch() 함수를 접해볼 것이고, 이들은 비동기로 동작한다는 소리를 한번 쯤은 들어본 적이 있을 것이다. 비동기는 메인 스레드가 작업을 다른 곳에 인가하여 처리되게 하고, 그 작업이 완료되면 콜백 함수를 받아 실행하는 방식으로, 쉽게 말해 작업을 백그라운드에 요청하여 처리되게 하여 멀티로 작업을 동시에 처리하는 것으로 보면 된다.

<p align="center">
<img src="../../images/javascript/asynchronous-2.png" width="600">
</p>

## 비동기처리 예제

```jsx
function func1() {
  console.log('func1')
  func2()
}

function func2() {
  setTimeout(function () {
    console.log('func2')
  }, 0)

  func3()
}

function func3() {
  console.log('func3')
}

func1()
```

위 예제는 비동기식으로 동작하는 코드로 순차적으로 실행되지 않는다.
위 예제를 실행하면 setTimeout 메소드에 두번째 인수 인터벌을 0초로 설정하여도 콘솔에 “func1 func2 func3”의 순서로 로그가 출력되지 않는다. 이는 setTimeout 메소드가 비동기 함수이기 때문이다.

함수 func1이 호출되면 함수 func1은 Call Stack에 쌓인다. 그리고 함수 func1은 함수 func2을 호출하므로 함수 func2가 Call Stack에 쌓이고 setTimeout가 호출된다. **setTimeout의 콜백함수는 즉시 실행되지 않고 지정 대기 시간만큼 기다리다가 “tick” 이벤트가 발생하면 태스크 큐로 이동한 후 Call Stack이 비어졌을 때 Call Stack으로 이동되어 실행된다.**

<p align="center">
<img src="../../images/javascript/asynchronous-3.png" width="600">
</p>
