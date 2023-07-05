# 웹표준(Web Standards)

## 웹표준이란?

---

- 웹표준은 웹에서 사용되는 기술들의 표준화를 의미힌다. 즉, 웹사이트를 구성하는 HTML, CSS, JavaScript 등의 언어들이 표준화된 방식으로 작성되어야 한다는 것.
- 사용자가 어떤 브라우저나 기기를 사용하더라도 동일한 컨텐츠를 볼 수 있도록 웹에서 표준적으로 사용되는 기술이나 규칙 → ‘동일한 컨텐츠’는 완벽히 똑같은 컨텐츠를 의미하는 것이 아닌, 모든 플랫폼에서 동등한 수준의 정보에 접근이 가능함을 의미한다.
- 웹표준은 W3C(World Wdie Web Consortium)이라는 조직의 토론에 의해 결정된다.

## 웹표준이 등장한 배경

---

- 웹 표준이 없던 1990년대 말 ~ 2000년대 초반에는 웹 사이트 개발자는 사실상 두 개의 사이트를 만들어야 했다. (익스플로러, 넷스케이프)
- 웹표준 문제의 대표적인 사례는 ActiveX
  ActiveX는 윈도우에서만 동작하는 플러그인으로, 맥이나 리눅스에서는 사용 불가했다. 우리나라의 금용 사이트나 쇼핑몰은 액티브액스를 통해 전자금융, 전자결제를 처리하는 경우가 많았는데, 크롬이나 사파리 같은 브라우저에서는 액티브액스를 설치할 수 가 없어서 인터넷익스플로러를 사용해야 했다.
  액티브엑스는 IE에서만 작동하는 비표준 기술로, 인터넷익스플로러의 점유율만 믿고 비표준 기술을 표준처럼 남용하고 고착시킨 결과였다.

## 웹표준의 장점

---

### 1. 웹페이지의 호환성(cross-browsing)

웹 표준으르 준수하면, 웹페이지가 모든 브라우저에서 일관적으로 표시된다. 이를 통해 사용자들은 어떤 브라우저를 사용하더라도 동일한 사용자 경험을 얻을 수 있어 오래된 브라우저에서도 컨텐츠가 적절하게 표시되고 호환성과 운용성이 확보된다.

### 2. 유지보수 및 확장

웹 표준을 준수하면, 웹페이지를 만드는데 필요한 시간과 비용을 줄일 수 있어 유지보수 및 확장성이 좋아진다. 또한 논리적으로 효율적으로 작성된 웹 문서는 코드의 양이 줄어 파일 크기가 줄고 서버 부담의 감소로 이어진다.

⇒ 브라우저와 OS에 관계없이 하나의 코드로 모든 플랫폼에 대응할 수 있어, 위의 두가지는 개발자입장에서는 개발의 효율성을, 기업에서는 서버 비용 절감과 운용의 효율성.

### 3. 검색 엔지 최적화(SEO)

검색 엔진 최적화란 웹페이지가 검색 결과에 좀 더 높은 순위가 나올 수 있도록 하는 작업을 의미한다. 웹 크롤러 봇은 웹페이지를 탐색하여 분류하는데 의미를 가진 시멘틱태그를 사용하는 등 표준을 지켜 웹페이지를 만들면, 크롤러 봇이 이해하기 쉬워져 더욱 잘 인식 할 수 있다.

### 4. 개발자가 더 쉽게 코드를 이해할 수 있다.

시멘틱태그처럼 의미있는 태그는 개발자가 더 쉽게 이해할 수 있게 돕는다. → 개발자의 효율을 높여줌.

### 5. 구조와 표현의 분리

HTML은 웹의 구조를, CSS는 웹의 표현을 담당하도록 분리되어 유지보수가 용이하다.

### 6. 웹 접근성 향상

웹 표준을 준수하면, 모든 사용자가 쉽게 웹 페이지에 접근할 수 있도록 웹 접근성을 고려할 수 있다. 예를 들어 다양한 브라우저, 휴대폰 PDA, 장애인 지원용 프로그램에서도 대응이 가능하므로 접근성이 향상되고 스크린리더기 등 보조공학 기기 사용자들이 조금 더 정확한 정보를 얻을 수 있도록 도움을 준다.

## 웹 표준의 기술

1. XHTML ( eXtensible Hypertext Markup Language )
2. CSS (Cascading Style Sheets)
3. XML (eXtensible Markup Language)
4. DOM(Document Object Model)
5. ECMAScript : ECMA international 의 ECMA-262 기술 명세에 정의된 표준화된 스크립트 프로그래밍 언어

## HTML5

---

### 1. DOCTYPE 선언

HTML 파일 최상단에 위치하는 태그. DOCTYPE은 어떤 버전의 HTML로 작성된 문서인지 브라우저에 알려준다. `<!DOCTYPE html>`은 문서가 HTML5 버전을 지켜 작성된 문서임을 뜻한다.
<p align="center">
<img src="../../images/frontend/web_standards_1.png" width="600">
</p>


### 2. 시멘틱 태그 사용 (Semantic tag)

- semantic은 ‘의미의, 의미가 있는’ 이라는 뜻으로, 시맨틱태그를 통해 요소의 의미를 고려하고 구조를 설계하여 웹 사이트 코드를 작성하는 것이다.
- 시맨틱 태그는 HTML5에서 새로 추가된 태그로, `<header>`, `<nav>`, `<section>`, `<body>` , `<footer>` 등의 태그를 사용하여 웹 페이지의 구조를 더욱 명확하게 표현할 수 있다.

### 3. HTML 규칙

- 확장자는 반드시 htm, html로 만들어야 한다.
- 파일이나 폴더명은 반드시 여백이 없는 영문자로 작성해야 한다.
- 태그는 반드시 시작 태그와 종료 태그를 지켜야 웹 브라우저가 인식할 수 있다.

## 웹 접근성(Web Accessibility)

---

- 웹 접근성은 **장애를 가진 사람들**도 신체적, 환경적 조건에 관계없이 인터넷을 통해 정보에 접근하고 이용할 수 있도록 하는 것을 말한다. 이는 인터넷을 더욱 공평하고 인종, 성별, 연령, 장애 유무와 상관없이 모두가 이용할 수 있는 공간으로 만드는 것을 목표로 한다.
- 시각장애인의 경우 화면을 눈으로 볼 수 없기 때문에 '스크린 리더'라는 별도의 소프트웨어를 컴퓨터에 설치하여 음성으로 웹페이지에 담긴 정보를 이해한다. 하지만 '스크린 리더'는 스스로 웹페이지의 내용을 분석하지 못한다. 따라서 스크린 리더가 읽을 수 있게 예로 들어 img 태그의 alt속성과 같은 스크린 리더가 읽을 수 있도록 해줘야 한다.

## 웹 콘텐츠 접근성 지침 (WCAG)

---

웹 콘텐츠 접근성 지침(WCAG)은 웹 접근성을 확보하기 위한 국제 표준으로, 다양한 장애를 가진 사용자들이 웹 사이트에 쉽게 접근하고 이용할 수 있도록 가이드라인 이라고 보면 된다.

WCAG는 4가지 원칙, 13가지 지침, 78가지 성공 기준으로 구성되어 있다.

### 1. 인식의 용이성

정보와 사용자 인터페이스 요소는 그들이 인지할 수 있도록 사용자에게 표시될 수 있어야 한다.

1. 텍스트가 아닌 콘텐츠에 대체 텍스트를 사람들이 원하는 인쇄, 점자, 음성, 기호 또는 간단 언어 등과 같은 형태로 제공해야 한다.
2. 정보와 구조의 손실 없이 콘텐츠를 다른 방식(예를 들면 더욱 간단한 형태로)들로 표현할 수 있어야 한다.
3. 사용자들이 보다 쉽게 보고 들을 수 있는 전경에서 배경을 분리한 콘텐츠를 만들어야 한다.

### 2. 운용의 용이성

사용자 인터페이스 요소와 탐색은 운용 가능해야 한다.

1. 키보드로 모든 기능을 사용할 수 있도록 해야 한다.
2. 읽기 및 콘텐츠를 사용하는 사용자에게 충분한 시간을 제공해야 한다.
3. 사용자가 탐색하고, 콘텐츠를 찾고 그들이 어디에 위치하고 있는지를 알 수 있도록 도와주는 방법을 제공해야 한다.

### 3. 이해의 용이성

정보와 사용자 인터페이스 운용은 이해할 수 있어야 한다.

1. 텍스트 콘텐츠를 판독하고 이해할 수 있도록 만들어야 한다.
2. 웹 페이지의 탑재와 운용을 예측 가능한 방법으로 제작해야 한다.
3. 사용자의 실수를 방지하고 수정할 수 있도록 도와야 한다.

### 4. 내구성

콘텐츠는 보조 기술을 포함한 넓고 다양한 사용자 에이전트에 의존하여 해석될 수 있도록 충분히 내구성을 가져야 한다.

1. 웹 기술 사용, 호환성 검사, 오류 정정 등

## 정리

---

개발하기 위해서는 코드짜고 예쁘게 홈페이지를 만드는 것도 중요하지만, 웹 표준 & 웹 접근성을 준수하여 사용자에게 더 편리하고 동등한 페이지를 제공할 수 있게 만들어야 한다.

참고

https://www.youtube.com/watch?v=xToJhmAJYCE  
[https://inpa.tistory.com/entry/WEB-📚-웹-표준의-이해](https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-%EC%9B%B9-%ED%91%9C%EC%A4%80%EC%9D%98-%EC%9D%B4%ED%95%B4)