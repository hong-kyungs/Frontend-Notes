# this

this는 함수 내에서 함수 호출 맥락(context)을 의미한다. 맥락이라는 것은 상황에 따라서 달라진다는 의미인데 즉, **함수를 어떻게 호출하느냐에 따라서 this가 가리키는 대상이 달라진다**는 뜻이다.

## 전역범위

전역 범위(Global context), 그러니까 JavaScript에서 가장 평범하게 일반적으로 `this`를 호출한다면, `this`는 `window`라는 전역 객체를 가리킨다(Node.js에서는 `Global`).

참고로 `Window` 객체라는 것은, 현재 실행되고 있는 JavaScript의 모든 변수, 함수, 객체, DOM 등을 포함하고 있는 객체로, 만물의 근원이 되는 객체이다.

```jsx
// 1. 전역 범위에서 호출
console.log(this) // Window {...}
```

## 함수범위

하지만 `this`를 함수 내에서 호출한다면 현재 실행되고 있는 코드의 문맥(Context)에 따라 `this`가 달라진다.

### 1. 단순함수호출

```jsx
// 1. 일반 함수 범위에서 호출
function outside() {
  console.log(this) // this는 window

  // 2. 함수 안에 함수가 선언된 내부 함수 호출
  function inside() {
    console.log(this) // this는 window
  }
  inside()
}
outside()
```

우선 가장 일반적인 방법으로 함수를 선언한 후 호출하는 경우, `this`는 `Window` 객체이다.

함수 안에서 또 함수를 선언하더라도, `this`는 여전히 `Window`이다.

### 2. 객체의 메소드(Method)

```jsx
// 1. 객체 또는 클래스 안에서 메소드를 실행한다면 this는 Object 자기 자신
var man = {
  name: 'john',
  hello: function () {
    // 2. 객체이므로 this는 man을 가리킴
    console.log('hello ' + this.name)
  },
}
man.hello() // 3. hello john
```

함수를 어떤 객체의 메소드로 호출하면 `this`의 값은 그 객체를 사용한다. 예제에서 `hello` 메소드는 객체 `man`에 소속되어 있고, 그 객체 `man`을 `this`로 접근할 수 있다.

함수를 객체 외부에서 선언하고, 객체 안에서 호출하는 경우에도 `this`는 해당 객체의 `this`를 참조한다. 위의 예시에 이어 아래 예시를 보세요.

```jsx
// 3. 일반 함수 welcome을 선언
function welcome() {
  // 4. 여기서 this는 전역 객체 Window이므로, 만약 실행시키면 undefined가 뜸
  console.log('welcome ' + this.name)
}

// 5. man 객체의 welcome 속성에 일반 함수 welcome을 추가
man.welcome = welcome

// 6. welcome이 man 객체에서 호출되었으므로 welcome john이 출력됨
man.welcome() // welcome john
```

이와는 반대로, 객체의 함수를 외부에서 호출할 때 `this`는 `Window`가 된다.

```jsx
// 7. man 객체의 thanks 속성에 함수를 선언
man.thanks = function () {
  // 8. man.thanks()를 호출하면 thanks john이 출력
  console.log('thanks ' + this.name)
}

// 8. 이 함수를 객체 외부에서 참조
var thankYou = man.thanks

// 9. 객체 외부이므로 this가 Window 객체가 되어서 thanks (undefined)가 출력
thankYou()

// 10. 그럼 또 다른 객체에서 이 함수를 호출하면 어떻게 될까?
women = {
  name: 'barbie',
  thanks: man.thanks, // 11. man.thanks 함수를 women.thanks에 참조
}

// 12. this가 포함된 함수가 호출된 객체가 women이므로 thanks barbie가 출력
women.thanks()
```

잠깐, 여기서 조심해야 할 점이 있다. 바로 메소드에서 내부 함수를 선언하는 경우는 `this`가 어떻게 될까요?

```jsx
var man = {
  name: 'john',
  // 1. 이것은 객체의 메소드
  hello: function () {
    // 2. 객체의 메소드 안에서 함수를 선언하는 것이니까 내부 함수
    function getName() {
      // 3. 여기서 this가 무엇을 가리키고 있을까?
      return this.name
    }
    console.log('hello ' + getName()) // 4. 내부 함수를 출력시키고
  },
}
man.hello() // 메소드를 실행시키면 undefined가 뜬다! this는 Window였던 것
```

객체의 메소드에서 `this`가 객체를 가리키고 있던 것과는 다르게, 내부 함수에서 `this`는 `Window` 객체를 가리키고 있다. 내부 함수는 엄밀히 말해 메소드가 아니기 때문에, 단순 함수 호출 규칙에 따라 `Window`를 가리키고 있다는 점에 유의해야 한다.

### 3. call(), apply(), bind()

`this`에 바인딩될 객체는 함수 호출 패턴에 의해 결정되는데, 자바스크립트 엔진의 암묵적 this 바인딩 이외에 this를 특정 객체에 명시적으로 바인딩하는 방법도 제공된다. 이것을 가능하게 하는 것이 `call(), apply(), bind()` 메소드이다.

```jsx
// 1. 이것은 객체의 메소드
var man = {
  name: 'john',
  // 2. 객체의 메소드 안에서 함수를 선언하는 것이니까 내부 함수
  hello: function () {
    function getName() {
      // 3. 여기서 this가 무엇을 가리키고 있을까?
      return this.name
    }
    // 4. 이번에는 call()을 통해 현재 문맥에서의 this(man 객체)를 바인딩해주었다
    console.log('hello ' + getName.call(this))
  },
}

// 이번에는 메소드를 실행시키면 john가 뜬다!
// this가 man 객체로 바인딩 된 것을 확인할 수 있다
man.hello()
```

```jsx
var obj2 = { c: 'd' }
function b() {
  console.log(this)
}
b() // Window
b.bind(obj2).call() // obj2
b.call(obj2) // obj2
b.apply(obj2) // obj2
```

`call`과 `apply`는 함수를 호출하는 함수이다. 그러나 그냥 실행하는 것이 아니라 첫 번째 인자에 `this`로 setting하고 싶은 객체를 넘겨주어 `this`를 바꾸고나서 실행한다.

`bind`함수가 `call`, `apply`와 달리 bind 함수는 함수가 가리키는 `this`만 바꾸고 호출하지는 않는 것이다.

### 4. 콜백 함수

```jsx
// 1. 콜백함수
var object = {
  callback: function () {
    setTimeout(function () {
      console.log(this) // 2. this는 window
    }, 1000)
  },
}
```

콜백 함수에서는 `this`가 `Window`를 가리킵니다. 객체 안에 메소드로 선언되어 있어도 마찬가지다. ⇒ **고차 함수의 콜백함수 안에서 this는 콜백함수가 일반 함수이기 때문에 전역 객체를 참조한다.**

### 5. 생성자

함수 앞에 `new` 키워드가 붙이고 선언할 때, `this`를 해당 객체에 바인딩한다.

```jsx
// 1. 클래스 역할을 할 함수 선언
function Man() {
  this.name = 'John'
}

// 2. 생성자로 객체 선언
var john = new Man()

// 3. this가 Man 객체를 가리키고 있어 이름이 정상적으로 출력된다
john.name // => 'John'
```

ECMAScript 6 문법인 `class`를 이용해 작성할 수도 있다.

```jsx
// 1. Class Man 선언
class Man {
  constructor(name) {
    this.name = name
  }
  hello() {
    console.log('hello ' + this.name)
  }
}

// 2. 생성자 실행
var john = new Man('John')
john.hello() // 3. hello John 출력
```

여기서 주의할 점은 `new` 키워드를 붙이지 않을 경우 일반 함수로 호출되어 `this`가 해당 객체로 바인딩 되지 않기 때문에 `Window` 객체를 건드리는 일이 발생할 수 있다. 따라서 `new` 키워드를 꼭 써줘야한다.

### 6. 화살표 함수(Arrow function)

화살표 함수는 ECMAScript 6에서 새로 추가된, 함수를 축약해서 사용할 수 있는 문법이다. 하지만 단순히 함수를 축약해서 사용하는 것 뿐만이 아니라 화살표 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정되고, `this`로 `window` 대신 상위 함수의 `this`를 가져온다.

`this`를 외부 스코프에서 정적으로 바인딩된 문맥(정적 컨텍스트, Lexical context)을 가진다는 특징이 있고, 정적 컨텍스트는 함수가 실행된 위치가 아닌, 정의(defined)된 위치에서의 컨텍스트를 참조한다.

```jsx
var object = {
    callback: function() => {
        setTimeout(() => {
            console.log(this); // this는 object
        }, 1000);
    }
}
```

```jsx
// 1. 화살표 함수
var obj = {
  a: this, // 2. 일반적인 경우 this는 window,
  b: function () {
    console.log(this) // 3. 메소드의 경우 this는 객체 obj
  },
  c: () => {
    console.log(this)
    // 4. 화살표 함수의 경우 정적 컨텍스트를 가짐, 함수를 호출하는 것과 this는 연관이 없음
    // 5. 따라서 화살표 함수가 정의된 obj 객체의 this를 바인딩하므로 this는 window
  },
}

obj.b() // 6. obj
obj.c() // 7. window
```

일반적인 방법으로 함수를 선언(`function () { ... }`)하면, 일반적인 함수는 함수가 실행될 때 자체적으로 `this`를 할당하게 되는데, 이 함수는 메소드 함수이므로 `this`가 메소드를 포함하는 객체로 바인딩된다.

하지만 화살표 함수는 `this`가 없기 때문에, 부모 스코프의 `this`를 바인딩하는데 위의 예시에서 이는 곧 `Window`객체를 의미한다. 따라서 메소드로 화살표 함수를 쓰면, `this`를 이용한 부모 객체에 접근할 수 없다.

참조

[[JavaScript 개발자라면 꼭 알아야 할 this – 재그지그의 개발 블로그](https://wormwlrm.github.io/2019/03/04/You-should-know-JavaScript-this.html)](https://wormwlrm.github.io/2019/03/04/You-should-know-JavaScript-this.html.html)  
[제로초](https://www.zerocho.com/category/JavaScript/post/5b0645cc7e3e36001bf676eb)
