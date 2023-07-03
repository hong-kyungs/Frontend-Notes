# JavaScript Data Type

### JavaScript 언어의 타입은 원시 값(_primitive value_)과  객체(_object_)로 나뉜다.

## primitive value(원시값)

---

- 더이상 작은 단위로 나뉘어질 수 없는 한가지 아이템. 원시 값은 **불변**하여 변형할 수 없다.(_immutable value_) - 원시값을 교체할 수는 있지만, 직접 변형할 수는 없다.
- **number, string, boolean, null, undefined, symbol, bigint**

### 1. Number

- javascript 에서 숫자에 하나의 형식만 있습니다. 숫자는 소수점과 함께 또는 없이 쓸 수 있습니다.
- `number` 라고 따로 선언하지 않아도 됨.

```jsx
let x1 = 34.0
let x2 = 34
console.log(`value: ${x1}, type: ${typeof x1}`) //value: 34, type: number
console.log(`value: ${x2}, type: ${typeof x2}`) //value: 34, type: number
```

- 숫자형엔 일반적인 숫자 외에 `Infinity`, `-Infinity`, `NaN` 같은 '특수 숫자 값(special numeric value)'이 포함됩니다. - `Infinity`는 무한대를 나타내고, `NaN`은 계산 중에 에러가 발생했다는 것을 나타내주는 값이다.

```jsx
const infinity = 1 / 0
const negativeInfinity = -1 / 0
const nAn = 'not a number' / 2
console.log(infinity) //Infinity
console.log(negativeInfinity) //-Infinity
console.log(nAn) //NaN
```

### 2. String, 문자열

자바스크립트에선 문자열(string)을 따옴표로 묶는다.

따옴표는 세 종류가 있다.

1. 큰따옴표: "Hello"
2. 작은따옴표: 'Hello'
3. 역 따옴표(백틱, backtick): \`Hello`

역 따옴표로 변수나 표현식을 감싼 후 `${…}`안에 넣어주면, 아래와 같이 원하는 변수나 표현식을 문자열 중간에 손쉽게 넣을 수 있습니다.

```jsx
let str = 'Hello'
let str2 = 'Single quotes are ok too'
let phrase = `can embed another ${str}` // can embed another Hello
```

### 3. Boolean

Boolean타입의 값은 논리적 참, 거짓을 나타내는 `true` 와 `false` 뿐입니다.

값이 없거나 `0`, `-0`, `null`, `false`, `NaN`, `undefined`, 빈 문자열 (`""`)이라면 객체의 초기값은 `false`가 됩니다.

### 4. null

`null`은 의도적으로 변수에 값이 없다는 것을 명시할때 사용한다.

### 5. undefined

선언 이후 값을 할당하지 않은 변수는 `undefined` 값을 가진다.

### 6. symbol

`심볼(symbol)`형은 객체의 고유한 식별자(unique identifier)를 만들 때 사용된다.

새로운 원시 심볼을 생성하려면 `Symbol()`을 호출하고, 모든 `Symbol()` 호출은 각각 고유한 심볼을 반환하는 것이 보장된다

```jsx
const sym1 = Symbol('foo')
const sym2 = Symbol('foo')
console.log(sym1 === sym2) // false
```

### 7. Bigint

`BigInt`는 `Number`가 나타낼 수 있는 최댓값인  **2^53 - 1** 보다 큰 정수를 표현할 수 있는 내장 객체이다. `Number`로 표현했을 때 `Infinity`가 되는 아주 큰 값도 `BigInt`로 정수 형태를 잃지 않고 표현할 수 있다.

⇒ 암호 관련 작업같이 아주 큰 숫자가 필요한 상황이거나 아주 높은 정밀도로 작업을 해야 할 때는 이런 큰 숫자가 필요합니다.

`BigInt`는 정수 리터럴의 뒤에 `n`을 붙이거나(`10n`) 함수 `BigInt()`를 호출해 생성할 수 있다.

```jsx
const theBiggestInt = 9007199254740991n
const alsoHuge = BigInt(9007199254740991)
// ↪ 9007199254740991n
```

참고

https://ko.javascript.info/types
https://developer.mozilla.org/ko/docs/Glossary/Primitive
[https://velog.io/@jenny87879/JavaScript-변수-데이터-타입의-종류](https://velog.io/@jenny87879/JavaScript-%EB%B3%80%EC%88%98-%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%83%80%EC%9E%85%EC%9D%98-%EC%A2%85%EB%A5%98)
