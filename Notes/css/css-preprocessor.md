# CSS preprocessor(CSS 전처리기)

## 📌 CSS preprocessor가 탄생한 이유

- **css는 웹 개발 작업이 커지면서 점점 불편함이 생긴다**

웹페이지를 만들 때 css 파일에 스타일을 정의한다. 그런데 웹 페이지가 점점 커지고 복잡해지면 정의하는 스타일도 굉장히 많아지게 되고, 선택자를 불필요하게 과다 사용하게 되는 등 코드가 지저분해질 수 있고, 유지 보수 측면에서 불리한 점이 생길 수 있다. 이를 해결하기 위해 등장한 것이 `css preprocessor` (css 전처리기) 다.

## 📌 CSS preprecessor(CSS 전처리기)

> A **CSS preprocessor** is a program that lets you generate CSS from the preprocessor's own unique syntax.
> **CSS 전처리기**는 전처리기가 가진 특별한 syntax으로 CSS를 생성하도록 하는 프로그램입니다.

CSS 전처리기(CSS Preprocessor)는 모듈별로 특별한 `Syntax`를 가지고 있고 여기에 `믹스인(mixin)`, `중첩 셀렉터(nesting selector)`, `상속 셀렉터(inheritance selector)` 등 Programmatically 한 요소를 접목해 방대해지는 CSS 문서의 양을 효율적으로 처리하고 관리해 주는 통합적인 단어를 말한다.
이 CSS 전처리기(CSS Preprocessor) 자체만으로는 웹 서버가 인지하지 못하기 때문에 각 CSS 전처리기에 맞는 `Compiler`를 사용해야 하고 컴파일을 하게 되면 실제로 우리가 사용하는 CSS 문서로 변환이 된다.

`CSS 전처리기(CSS Preprocessor)`는 CSS 문서의 작성에 도움을 주는 도구이다.
우리가 흔히 CSS 문서 작성할 때는 많은 반복적인 작업을 요구하고 Color 값을 찾는 일, tag를 닫는 일 등 번거로운 작업 역시 포함되어있다. 그뿐만 아니라 클래스의 상속과 같은 사항으로 점점 CSS 문서는 양이 많아지고 이로 인해서 이후 유지관리에 많은 영향을 준다.
이런 CSS의 문제점들을 Programmatically 한 방식. 즉 변수, 함수, 상속 등 일반적인 프로그래밍 개념을 사용하여 해결해 나갈 수 있다.

CSS 전처리기(CSS Preprocessor)에는 다양한 모듈이 존재하고 가장 많이 사용되는 전처리기에는 `Sass`, `Less`, `Stylus`가 있으며, 서로의 특징에 맞게 약간의 Syntax만 다를 뿐 개념 자체는 동일하기 때문에 Learning curve가 낮은 편이다.

## 📌 장점

> 1.  재사용성 - 공통 요소 또는 반복적인 항목을 변수 또는 함수로 대체
> 2.  시간적 비용 감소 - 임의 함수 및 Built-in 함수로 인해 개발 시간적 비용 절약
> 3.  유지 관리 - 중첩, 상속과 같은 요소로 인해 구조화된 코드로 유지 및 관리가 용이

### 1. 재사용성

**재사용성**의 장점을 가장 쉽게 파악하는 방법은 `CSS에서 color를 지정`하는 방법을 생각해보자. 우리가 특정 클래스에 color 속성을 주고 값을 지정할 때 `hex code` 또는 `RGB`로 지정을 한다. 하지만 특정 색상이 반복된다면 우리는 주기적으로 색상 코드를 찾고 반영을 해줘야 한다. 하지만 CSS 전처리기(CSS Preprocessor)에서는 이런 반복되는 부분을 변수로 처리할 수 있다. 대부분 실무에서는 하나의 파일 안에 `color-set`을 모두 정의하여 사용된다.

```jsx
$primary-color: #fff

.class-A
    background-color: $primary-color

.class-B
    background-color: $primary-color
```

### 2. 시간적 비용 감소

각 CSS 전처리기(CSS Preprocessor)에는 `내장함수(Built-in Functions)`가 존재한다. 이 내장 함수는 이미 전처리기 내에 포함된 함수로 우리는 필요한 값들만 전달하면 이에 대한 결과를 생성해 준다. 예를 들어 `darken(color, amount)`이라는 내장 함수는 색상과 퍼센티지를 지정해 주면 거기에 알맞은 값을 출력해 준다.

```jsx
$color: #2ecc71
$buttonDark: darken($buttonColor, 10%)

button
    background: $color
    box-shadow: 0px 5px 0px $buttonDark
```

### 3. 유지 관리

**유지 관리**는 가장 중요하고 눈에 띄는 장점 중의 하나이다.

클래스를 정의하다 보면 상속과 공통 속성을 지정하기 위해서 무지막지하게 길게 정의를 한다. 이런 이유로 CSS 문서가 가독성이 매우 떨어지는 이유 중 하나이다. 이런 내용을 CSS 전처리기(CSS Preprocessor)에서는 `중첩(Nesting)`과 `상속(Extend)`을 통해 구조화 할 수 있다.

**중첩(Nesting)**

```jsx
.class-A
    width: 100%

    .A-child-1
        color: red


    .A-child-2
        color: blue
```

위 내용을 컴파일하게 되면 아래와 같다.

```jsx
.class-A {
    width: 100%
}

.class-A .A-child-1 {
    color: red
}

.class-A .A-child-2 {
    color: blue
}
```

**상속(Extend)**

```sass
.class-A
    color: red
    padding: 10px

.class-B
    @extend .class-A
    border: 1px solid red

```

위 내용을 컴파일하게 되면 아래와 같다.

```css
.class-A, .class-B {
    color: red
    padding: 10px
}

.class-B {
    border: 1px solid red
}
```

## 📌 단점

성능, 사용성 등 단점을 찾고 있겠지만 가장 중요한 것 중 하나가 실무에서의 사용이다. 그리고 이 내용이 곧 단점이 되기도 하다. 실무에서는 대부분 `CSS의 작업(Publishing)`은 `퍼블리셔(Publisher)` 또는 `디자이너(Designer)`가 진행하게 된다. 물론 Front-End 개발자가 진행하는 경우도 있지만 좀 더 체계가 필요한 회사나 프로젝트에서는 퍼블리셔나 디자이너가 퍼블리싱 작업을 하는 경우가 있는데 퍼블리셔나 디자이너가 개발에 대한 역량과 요소를 알아야 한다는 것이 문제이다. 지금까지 말했지만, CSS 전처리기(CSS Preprocessor)는 Programmatically 한 요소를 접목했기 때문에 분기문 처리, 변수의 이해, mixin의 이해 등 개발적인 요소를 알아야 하기 때문이다. Learning curve가 낮다는 장점은 순전히 개발자에 한해서이다.

- 전처리기를 위한 도구 필요
- 퍼블리셔나 디자이너가 개발에 대한 역햘과 요소 접목으로 개발적인 요소 알아야 함→ 개발자에 한해서만 Learning curve 낮음

참조  
https://chanhuiseok.github.io/posts/web-5/  
https://kdydesign.github.io/2019/05/12/css-preprocessor/
