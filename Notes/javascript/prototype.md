# 프로토타입(prototype)

## 프로토타입이란?

자바스크립트의 모든 객체는 프로토타입(prototype)이라는 객체를 가지고 있다.
자바스크립트의 모든 객체는 자신의 부모 역할을 담당하는 객체와 연결되어 있다. 그리고 이것은 객체 지향의 상속 개념과 같이 부모 객체의 프로퍼티 또는 메소드를 상속받아 사용할 수 있게 한다. 이러한 부모 객체를 **Prototype(프로토타입) 객체** 또는 줄여서 Prototype(프로토타입)이라 한다.

Prototype 객체는 생성자 함수에 의해 생성된 각각의 객체에 공유 프로퍼티를 제공하기 위해 사용한다.

## [[Prototype]] vs prototype 프로퍼티

모든 객체는 자신의 프로토타입 객체를 가리키는 [[Prototype]] 인터널 슬롯(internal slot) 을 갖으며 상속을 위해 사용된다.

함수도 객체이므로 [[Prototype]] 인터널 슬롯을 갖는다. 그런데 함수 객체는 일반 객체와는 달리 prototype 프로퍼티도 소유하게 된다.

> 주의해야 할 것은 prototype 프로퍼티는 프로토타입 객체를 가리키는 [[Prototype]] 인터널 슬롯은 다르다는 것이다. prototype 프로퍼티와 [[Prototype]]은 모두 프로토타입 객체를 가리키지만 관점의 차이가 있다.

```jsx
function Person(name) {
  this.name = name
}
var foo = new Person('Lee')

console.dir(Person) // prototype 프로퍼티가 있다.
console.dir(foo) // prototype 프로퍼티가 없다.
```

- [[Prototype]]
  - 함수를 포함한 모든 객체가 가지고 있는 인터널 슬롯이다.
  - **객체의 입장에서 자신의 부모 역할을 하는 프로토타입 객체를 가리키며 함수 객체의 경우 `Function.prototype`를 가리킨다.**

```jsx
console.log(Person.__proto__ === Function.prototype)
```

- prototype 프로퍼티
  - 함수 객체만 가지고 있는 프로퍼티이다.
  - **함수 객체가 생성자로 사용될 때 이 함수를 통해 생성될 객체의 부모 역할을 하는 객체(프로토타입 객체)를 가리킨다.**

```jsx
console.log(Person.prototype === foo.__proto__)
```

## 프로토타입 체인(prototype chain)

자바스크립트에서는 객체 이니셜라이저를 사용해 생성된 같은 타입의 객체들은 모두 같은 프로토타입을 가집니다.
또한, new 연산자를 사용해 생성한 객체는 생성자의 프로토타입을 자신의 프로토타입으로 상속받습니다

```jsx
var obj = new Object() // 이 객체의 프로토타입은 Object.prototype입니다.
var arr = new Array() // 이 객체의 프로토타입은 Array.prototype입니다.
var date = new Date() // 이 객체의 프로토타입은 Date.prototype입니다.
```

하지만 Object.prototype 객체는 어떠한 프로토타입도 가지지 않으며, 아무런 프로퍼티도 상속받지 않습니다.
또한, 자바스크립트에 내장된 모든 생성자나 사용자 정의 생성자는 바로 이 객체를 프로토타입으로 가집니다.

```jsx
var date = new Date() // 이 객체는 Date.prototype 뿐만 아니라 Object.prototype도 프로토타입으로 가집니다.
```

위와 같이 프로토타입이 상속되는 가상의 연결 고리를 프로토타입 체인(prototype chain)이라고 합니다.
Object.prototype 객체는 이러한 프로토타입 체인에서도 가장 상위에 존재하는 프로토타입입니다.

## 프로토타입의 생성

프로토타입을 생성하는 가장 기본적인 방법은 객체 생성자 함수(object constructor function)를 작성하는 것입니다.
생성자 함수를 작성하고 new 연산자를 사용해 객체를 생성하면, 같은 프로토타입을 가지는 객체들을 생성할 수 있습니다.

```jsx
function Dog(color, name, age) {
  // 개에 관한 생성자 함수를 작성함.
  this.color = color // 색에 관한 프로퍼티
  this.name = name // 이름에 관한 프로퍼티
  this.age = age // 나이에 관한 프로퍼티
}

var myDog = new Dog('흰색', '마루', 1) // 이 객체는 Dog라는 프로토타입을 가짐.

console.log(
  '우리 집 강아지는 ' +
    myDog.name +
    '라는 이름의 ' +
    myDog.color +
    ' 털이 매력적인 강아지입니다.',
)
//우리 집 강아지는 마루라는 이름의 흰색 털이 매력적인 강아지입니다.
```

## 프로토타입에 프로퍼티 및 메소드 추가하는 방법

### 1. 프로토타입에 프로퍼티 및 메소드추가

프로토타입의 경우에는 생성자 함수에 직접 추가해야만 이후에 생성되는 모든 다른 객체에도 적용할 수 있습니다.

```jsx
function Dog(color, name, age) {
  this.color = color
  this.name = name
  this.age = age
  this.family = '시베리안 허스키' // 프로토타입에 프로퍼티를 추가할 때에는 기본값을 가지게 할 수 있음.
  this.breed = function () {
    return this.color + ' ' + this.family
  }
}

var myDog = new Dog('흰색', '마루', 1)
var hisDog = new Dog('갈색', '콩이', 3)

console.log(
  '우리 집 강아지는 ' +
    myDog.family +
    '이고, 친구네 집 강아지도 ' +
    hisDog.family +
    '입니다.',
)
//우리 집 강아지는 시베리안 허스키이고, 친구네 집 강아지도 시베리안 허스키입니다.
```

### 2. prototype 프로퍼티

prototype 프로퍼티를 이용하면 현재 존재하고 있는 프로토타입에 새로운 프로퍼티나 메소드를 손쉽게 추가할 수 있습니다.

```jsx
function Dog(color, name, age) {
  this.color = color
  this.name = name
  this.age = age
}

// 현재 존재하고 있는 Dog 프로토타입에 family 프로퍼티를 추가함.
Dog.prototype.family = '시베리안 허스키'
// 현재 존재하고 있는 Dog 프로토타입에 breed 메소드를 추가함.
Dog.prototype.breed = function () {
  return this.color + ' ' + this.family
}

var myDog = new Dog('흰색', '마루', 1)
var hisDog = new Dog('갈색', '콩이', 3)

console.log(
  '우리 집 강아지는 ' +
    myDog.family +
    '이고, 친구네 집 강아지도 ' +
    hisDog.family +
    '입니다.',
)
//우리 집 강아지는 시베리안 허스키이고, 친구네 집 강아지도 시베리안 허스키입니다.
console.log('우리 집 강아지의 품종은 ' + myDog.breed() + '입니다.<br>')
//우리 집 강아지의 품종은 흰색 시베리안 허스키입니다.
console.log('친구네 집 강아지의 품종은 ' + hisDog.breed() + '입니다.')
//친구네 집 강아지의 품종은 갈색 시베리안 허스키입니다.
```

참조

https://poiemaweb.com/js-prototype  
http://www.tcpschool.com/javascript/js_object_prototype
