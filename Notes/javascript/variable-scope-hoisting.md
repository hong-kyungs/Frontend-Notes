# 변수, 스코프, 호이스팅

## 변수(variable)

---

변수(variable)는 데이터를 저장할 때 쓰이는 ‘이름이 붙은 저장소’

JavaScript에서 변수 선언 방식은  `var`, `let`, `const` 3가지가 있다.

### 변수의 선언과 할당

- name 이라는 변수를 선언(_declaration_), name 이라는 변수에 JavaScript라는 값을 할당.

```jsx
let name = 'JavaScript'
```

### 1. var : 중복선언가능

```jsx
var name = 'javascript'
console.log(name) // javascript

var name = 'react'
console.log(name) // react
```

- `var` 로 선언한 변수는 동일한 이름으로 여러 번 중복해서 선언이 가능함. 이와 같은 경우, 마지막에 할당된 값이 변수에 저장됨. 위의 예제를 보면 에러 없이 각기 다른 값이 출력되는 것을 볼 수 있다.
- 이는 필요할 때마다 변수를 유연하게 사용할 수 있다는 장점이 될 수도 있지만, 기존에 선언해둔 변수의 존재를 잊고 값을 재할당하는 등의 실수가 발생할 가능성이 크다.. 특히 코드량이 많아졌을 때, 같은 이름의 변수명이 여러 번 선언되었다면 어디 부분에서 문제가 발생하는지 파악하기 힘들뿐더러 값이 바뀔 우려가 있다.
- 블록 스코프도 적용되지 않고 호이스팅 문제가 발생할 수 있다.
- 이를 보완하기 위해 ES6부터 추가된 변수 선언 방식이 `let` 과 `const` 임.

### 2-1. let : 중복 선언 불가능, 재할당 가능

```jsx
let name = 'javascript'
console.log(name) // javascript

let name = 'react'
console.log(name)
// Uncaught SyntaxError: Identifier 'name' has already been declared

name = 'vue'
console.log(name) // vue
```

- `var` 와 다르게 `let` 은 해당 변수가 이미 선언되었다는 에러 메시지가 출력된다.. 이처럼 중복 선언이 불가능하다.
- `name = 'vue'` 와 같이 변수 선언 및 초기화 이후 반복해서 다른 값을 재할당 할 수는 있다.

### 2-2. const : 중복 선언 불가능, 재할당 불가능

```jsx
const name = 'javascript'
console.log(name) // javascript

const name = 'react'
console.log(name)
// Uncaught SyntaxError: Identifier 'name' has already been declared

name = 'vue'
console.log(name)
// Uncaught TypeError: Assignment to constant variable
```

- let 과 const 의 차이점은 immutable 의 여부임. let 은 변수에 다른 값을 재할당할 수 있지만, const 는 재할당 시 에러 메시지가 출력됨. → const는 값을 한번 할당하면 절대 바뀌지 않는다.

```jsx
function func() {
  const list = ['A', 'B', 'C']

  list = 'D'
  console.log(list)
  // TypeError: Assignment to constant variable

  list.push('D')
  console.log(list) // ["A", "B", "C", "D"]
}
```

- 이처럼 `const` 는 constant(상수)를 뜻하기 때문에 한 번만 선언이 가능하며 값을 바꿀 수도 없음. 하지만 위 예제와 같이 배열과 오브젝트의 값을 변경하는 것은 가능함.
- 결과적으로 `const` 는 불변을 의미하는 것과 다르게, 값을 재할당하는 코드만 불가능하다고 볼 수 있음.

⇒ **`const` 를 기본으로 사용하여 불필요한 변수의 재사용을 방지하고, 재할당이 필요한 경우 `let` 을 사용하는 것이 좋음.**

## 스코프 (Scope)

---

스코프란 유효한 참조 범위를 뜻하며, 기존의 방법인 `var` 로 선언한 변수와 `let` 또는 `const` 로 선언한 변수의 스코프는 다르다.

### 1. var : 함수 레벨 스코프 (function-level scope)

```jsx
function func() {
  if (true) {
    var a = 5
    console.log(a) // 5
  }
  console.log(a) // 5
}

func() // 5
console.log(a) // ReferenceError: a is not defined
```

- 함수 내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다. 즉, 함수 내부에서 선언한 변수는 지역 변수이고 함수 외부에서 선언한 변수는 모두 전역 변수로 취급됨.

### 2. let, const : 블록 레벨 스코프 (block-level scope)

```jsx
function func() {
  if (true) {
    let a = 5
    console.log(a) // 5
  }
  console.log(a) // ReferenceError: a is not defined
}

console.log(a) // ReferenceError: a is not defined
```

- 함수, if문, for문, while문, try/catch문 등의 모든 코드 블록 ({...}) 내부에서 선언된 변수는 코드 블록 내에서만 유효하며 코드 블록 외부에서는 참조할 수 없다. 즉, 코드 블록 내부에서 선언한 변수는 지역 변수로 취급된다.

## 호이스팅(hoisting)

---

- 호이스팅이란 함수 내부에 있는 선언들을 모두 끌어올려 해당 함수 유효 범위의 최상단에 선언하는 것을 뜻한다. (실제로 코드가 끌어올려지는 것이 아닌, 자바스크립트 Parser가 함수 실행 전 해당 함수를 한 번 훑는 과정에서 내부적으로 끌어올려 처리하는 것을 뜻하며 실제 메모리에서는 변화가 없음) => 미리 선언문을 실행해둔다고 이해하면 된다.

### 1. var, 함수선언문 : 호이스팅이 발생함

```jsx
/* 변수 호이스팅 */
console.log(a) // undefined

var a = 5
console.log(a) // 5

/* 함수 호이스팅 */
foo() // foo

function foo() {
  console.log('foo')
}
```

- 변수 `a` 가 선언되기 전에 참조되었음에도 에러가 발생하지 않는다.
  이는 코드 실행 전에 자바스크립트 내부에서 미리 변수를 선언하고 undefined 로 초기화를 해두었기 때문이다. 함수선언문 또한 동일하게 선언되기 전 호출됨에도 에러가 발생하지 않는다.

### 2. let, const, 함수표현식 : 호이스팅이 발생하지만, 다른 방식으로 작동됨

```jsx
/* 변수 호이스팅 */
console.log(a) // ReferenceError: a is not defined

let a = 5
console.log(a) // 5

/* 함수 호이스팅 */
foo() // error

var foo = function () {
  console.log('foo')
}
```

- 변수 `a` 가 선언되기 전에 참조하니 에러가 발생한다.
  이는 호이스팅이 발생하지 않는 것이 아닌, 변수의 선언과 초기화 사이에 일시적으로 변수 값을 참조할 수 없는 구간인 TDZ(Temporal Dead Zone)에 빠졌기 때문에 보이는 현상임.
- 함수표현식을 사용하거나 `let` 또는 `const` 로 변수를 선언하는 경우, 자바스크립트 내부에서는 코드 실행 전 변수 선언만 해둘뿐 초기화는 코드 실행 과정에서 변수 선언문을 만났을 때 수행한다. 그렇기 때문에 호이스팅이 발생하기는 하지만, 값을 참조할 수 없기 때문에 동작하지 않는 것처럼 보이는 것이다.

참조

https://ko.javascript.info/variables  
https://80000coding.oopy.io/e1721710-536f-43f2-823b-663389f5fbfa
