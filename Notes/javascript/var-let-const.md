# var - let - const

## var 와 let의 차이

변수는 **스코프** (scope, 범위)라는 것을 가진다. var는 함수 스코프, let은 블록 스코프를 가진다.
여기서 scope란 변수에 접근 가능한 범위.

```jsx
function b() {
	var a = 1;
}

console.log(a);
> Uncaught ReferenceError: a is not defined

//a는 함수안에서 선언한것이고, 함수밖에서는 접근이 안된다.
```

a를 콘솔로 출력하면 에러가 발생한다. a는 함수 안에 선언된 변수이므로 함수 바깥에서는 접근할 수 없다. 이렇듯 함수를 경계로 접근 여부가 달라지는 것을 **함수 스코프**라고 한다.

if 문 안에 var를 넣어보면,

```jsx
if (true) {
  var a = 1
}
console.log(a) // 1
```

var는 함수 스코프(함수만 신경 씀)라서 if 문 안에 들어 있으면 바깥에서 접근할 수 있다. 그런데 let은 다르다.

```jsx
if (true) {
	let a = 1;
}
console.log(a);
> Uncaught ReferenceError: a is not defined
```

let의 경우에는 에러가 발생한다.

바로 let이 **블록 스코프**(블록을 신경 씀)라서 그렇다. 블록 if 문, for 문, while 문, 함수에서 볼 수 있는 { }를 의미합니다. 블록 바깥에서는 블록 안에 있는 let에 접근할 수 없습니다. const도 let과 마찬가지로 블록 스코프를 가진다.

## var / let / const

|                      | var | let | const |
| -------------------- | --- | --- | ----- |
| global scope         | yes | no  | no    |
| script scope         | no  | yes | yes   |
| function local scope | yes | yes | yes   |
| block scope          | no  | yes | yes   |
| 재선언               | yes | no  | no    |
| 재할당               | yes | yes | no    |

참조  
[생활코딩](https://www.youtube.com/watch?v=61iolhWgQt0&t=293s)
