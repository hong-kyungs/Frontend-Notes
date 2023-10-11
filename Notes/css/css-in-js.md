# CSS-in-JS

## 📌 CSS 어떤 방식이 좋을까?

HTML(Hypertext Markup Language)이 처음 등장한 1991년에는 CSS(Cascading Style Sheets)가 없었습니다. 웹 이용자들이 늘어나면서 디자인에 대한 요구가 커졌고 웹 고안자들은 HTML을 꾸며주는 언어의 필요성을 공감하게 되었습니다. 그렇게해서 CSS가 나오게 됩니다.

하지만 웹이 점점 복잡해지고 동적 기능 요구가 증가하면서 HTML과 CSS만으로는 화면의 모든 스타일을 제어하는 것은 어려워졋습니다.

이를 해결하기 위한 여러 가지 웹 애플리케이션 스타일 구성 방식 크게 두 갈래로 나눠지게 됩니다. 바로 CSS-in-JS와 CSS-in-CSS 입니다.

## 📌 CSS-in-CSS?

CSS코드를 모듈화하여 사용하는 방식입니다. CSS와 클래스 이름을 만들어 스코프를 지역적으로 제한하면서, 모듈을 불러옵니다. 이 과정에서 개발자가 지정했던 클래스 이름과 객체가 반환되는 방식으로 작동하게 됩니다.

모듈화 되지 않은 CSS를 사용하게 된다면 협업 과정에서 클래스 이름이 겹치게 될 때, 스코프 오염이 일어날 수 있는데, 모듈화에선 CSS 클래스 이름이 중복되어도 새로운 이름이 입혀져 중복 및 관리의 위험성이 적어지게 된다. 다만, 여러 파일에 나뉘어서 작성하기 때문에 많은 CSS 파일을 만들어 관리해야하는 단점이 있게 됩니다.

## 📌 CSS-in-JS?

CSS-in-JS는 스타일 정의를 css나 scss 파일이 아닌 JavaScript로 작성된 컴포넌트에 바로 삽입하는 스타일 기법이다.

기존 웹사이트는 HTML, CSS, JavaScript를 각자 별도의 파일로 두었는데, React나 Vue, Angluar와 같은 모던 자바스크립트 라이브러리가 인기를 끌고 컴포넌트 기발 개발 방법의 주류가 됨에 따라 한 컴포넌트에 HTML, CSS, JavaScript를 모두 포함하는 패턴이 많이 사용되고 있다.

2014년 처음 나오게 됐고, 다음과 같은 문제를 해결하기 위해 나온 기술입니다.

- Global namespace: 글로벌 공간에 선언된 이름의 명명 규칙 필요
- Dependencies: CSS간의 의존 관계를 관리
- Dead Code Elimination: 미사용 코드 검출
- Minification: 클래스 이름의 최소화
- Sharing Constants: JS와 CSS의 상태 공유
- Non-deterministic Resolution: CSS 로드 우선 순위 이슈
- Isolation: CSS와 JS의 상속에 따른 격리 필요 이슈

이 방법을 사용하기 위해 여러 라이브러리가 출시 되었고, 대표적으로는 styled-components, emotion 등의 라이브러리가 있습니다.

## 📌 inline-style 과의 차이점?

언뜻보면 CSS-in-JS는 컴포넌트 안에 css를 정의하는 inline-style과도 비슷한 느낌이다. 하지만 inline-style에는 다음과 같은 단점이 있으므로 inline-style의 사용은 지양하는 것이 좋다.

- 다시 렌더링 될때마다 스타일 객체가 다시 계산되어 성능이 저하될 수 있다.
- CSS 속성의 중복, 재사용성이 떨어진다
- inline-style로는 의사 클래스, 의사 요소, 미디어 쿼리, 키 프레임 애니메이션 같은 CSS의 기능을 활용할 수 없다
- 앱의 규모가 커질수록 유지 보수가 어렵다
- 인라인 스타일이 많으면 코드 가독성이 떨어진다

## 📌 CSS-in-JS의 장점

- CSS의 컴포넌트화로 스타일시트의 파일을 유지보수 할 필요가 없다. CSS 모델을 문서 레벨이 아닌 컴포넌트 레벨로 추상화한다 (모듈성)
- CSS-in-JS는 JavaSript 환경을 최대한 활용 할 수 있다
- JavaScript와 CSS 사이의 상수와 함수를 쉽게 공유 할 수 있다
- 현재 사용중인 스타일만 DOM에 포함한다.
- CSS-in-JS는 짧은 길이의 유니크한 클래스를 자동으로 생성하기 때문에 코드 경량화의 장점이 있다

## 📌 CSS-in-JS의 단점

- 러닝 커브
- 새로운 의존성
- 별도의 라이브러리를 설치해야 하므로 번들 크기가 커진다
- 인터랙션한 페이지일 경우 CSS 파일을 따로 관리하는 방법에 비해 느린 성능을 보여줄 수 있다.

참조  
[https://velog.io/@willy4202/styled-components의-사용이유를-알아보자.-css-in-js](https://velog.io/@willy4202/styled-components%EC%9D%98-%EC%82%AC%EC%9A%A9%EC%9D%B4%EC%9C%A0%EB%A5%BC-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90.-css-in-js)
https://jongminfire.dev/css-in-js.
https://blog.eunsukim.me/posts/introducing-css-in-js
