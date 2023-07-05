# 함수선언(declaration) 과 함수표현식(expression), 화살표 함수(arrow function)

## 함수 선언 (function declaration)

---

함수를 생성한다.

**_function 함수명 ( ) { }_**

```jsx
//함수 선언되기 호출가능 - 호이스팅
sayHi() //Hi

//함수 선언문
function sayHi() {
  console.log('Hi')
}

//함수 호출
sayHi() //Hi
```

- 호이스팅이란 선언문 자체가 해당 스코프의 최상위로 올려지는 현상으로, 함수 선언은 호이스팅이 일어난다. - 함수의 위치에 상관없이 어디서나 호출 가능하다.
- 만약 동일한 변수명으로 서로 다른 값을 할당할 경우 나중에 할당한 값이 먼저 할당한 값을 덮어씌우는 상황이 생긴다. 따라서 코드를 실행하는 중에 실제로 호출되는 함수는 오직 마지막에 할당한 함수, 즉 맨 마지막에 선언된 함수뿐이다. 하지만 이러한 상황에서 함수는 아무런 에러를 내지 않는다. 그렇기 때문에 이런 상황으로 에러가 나도 쉽게 찾을 수 없다.

## 함수 표현식(function expression)

---

함수를 변수에 할당한다.

**_const 변수명 = function () {}_** or **_const 변수명 = () ⇒ {}_**

```jsx
//함수 선언전에 호출시 에러
sayHello() //Error

// 함수 선언문
let sayHello = function () {
  // 이름이 없는 함수를 anonuymous 함수라고 한다.
  console.log('Hello!')
}

// 함수 호출
sayHello() //Hello
```

- 호이스팅의 영향을 받지않아 함수 선언 후 그 아래의 코드에서만 호출이 가능하다.

### 함수표현식 장점

- 호이스팅에 영향을 받지 않는다.
- 클로져로 사용 가능하다.
- 콜백으로 사용할 수 있다.(다른 함수의 인자로 넘길 수 있음)

⇒ 함수 표현식과 함수 선언식. 둘 중에 어느 것 하나가 항상 우월하다고 말할 수는 없다. 이 둘의 차이를 명확하게 이해하고 구분해서 상황에 따라, 필요에 따라 적절하게 활용하는 것이 좋다.

## 화살표 함수(arrow function)

---

- 함수 표현식을 단순하고 간결하게 해준다. ( 항상 이름이 없는 anonymous function이다.)

1. 한줄인 경우 block 없이, return 생략하고 작성이 가능하다.

```jsx
//function expression
const add = function (a, b) {
  return a + b
}
//arrow function 으로 아래와 같이 줄여서 쓸 수 있다.
const add = (a, b) => a + b
```

1. 여러줄인 경우 block을 사용하고 return 값을 꼭 넣어준다.

```jsx
let add = (a, b) => {
  // 중괄호는 본문 여러 줄로 구성되어 있음을 알려줍니다.
  let result = a + b
  return result // 중괄호를 사용했다면, return 지시자로 결괏값을 반환해주어야 합니다.
}
```

참조

https://bigtop.tistory.com/40.  
https://mihee0703.tistory.com/151.  
https://blog.naver.com/dev_wise/222600775722.
