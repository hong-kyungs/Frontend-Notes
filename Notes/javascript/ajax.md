# AJAX

## 📌 AJAX란?

Ajax란 Asynchronous JavaScript and XML의 약자로, 자바스크립트를 이용해서 비동기적(Asynchronous)으로 서버와 브라우저가 데이터를 교환할 수 있는 통신 방식을 의미한다.

Ajax는 **웹 페이지 전체를 다시 로딩하지 않고도, 웹 페이지의 일부분만을 갱신할 수 있다.** 즉 Ajax를 이용하면 **백그라운드 영역에서 서버와 통신하여, 그 결과를 웹 페이지의 일부분에만 표시할 수 있다.**

이때 서버와는 다음과 같은 다양한 형태의 데이터를 주고받을 수 있습니다.

- JSON
- XML
- HTML
- 텍스트 파일 등

## 📌\*AJAX 사용 사례

AJAX를 사용하여 웹 애플리케이션에서 다양한 기능을 만들 수 있습니다.

### 1. 자동 완성

검색 엔진은 사용자가 검색 창에서 특정 키워드를 검색할 때 실시간으로 자동 완성 옵션을 제공합니다. AJAX를 사용하면 웹 페이지가 각 문자 입력을 웹 서버로 릴레이하고 기존 페이지의 관련 권장 사항 목록을 반환할 수 있습니다.

### 2. 양식 검증

AJAX를 사용하면 웹 애플리케이션이 사용자가 양식을 제출하기 전에 양식의 특정 정보를 확인할 수 있습니다. 예를 들어 새 사용자가 계정을 만들면 웹 페이지는 사용자가 다음 섹션으로 이동하기 전에 사용자 이름을 사용할 수 있는지 자동으로 확인할 수 있습니다.

### 3. 채팅 기능

텍스트 메신저와 챗봇은 AJAX를 사용하여 브라우저에 실시간 대화를 표시합니다. AJAX는 사용자가 작성한 텍스트를 서버로 전송하고 다른 사용자의 채팅 인터페이스에 동시에 게시합니다.

### 4. 소셜 미디어

소셜 미디어 플랫폼은 AJAX를 사용하여 브라우저에 새 페이지를 로드하지 않으면서 최신 콘텐츠로 사용자의 피드를 업데이트합니다. 예를 들어 Twitter는 내가 팔로우하는 누군가가 새 소식을 트윗할 때마다 피드를 즉시 새로 고칩니다.

### 5. **투표 및 등급 시스템**

일부 포럼 및 소셜 북마킹 사이트는 AJAX를 사용하여 특정 게시물의 등급 또는 투표 결과를 실시간으로 표시합니다. 예를 들어 Reddit에서는 전체 페이지를 새로 고치지 않고도 게시물에 찬성 또는 반대 투표를 할 수 있습니다.

## 📌 Ajax의 장점

1. 웹 페이지 전체를 다시 로딩하지 않고도, 웹 페이지의 일부분만을 갱신할 수 있습니다.

2. 웹 페이지가 로드된 후에 서버로 데이터 요청을 보낼 수 있습니다.

3. 웹 페이지가 로드된 후에 서버로부터 데이터를 받을 수 있습니다.

4. 백그라운드 영역에서 서버로 데이터를 보낼 수 있습니다.

## 📌 Ajax의 한계

Ajax를 이용하면 여러 장점을 가지지만, Ajax로도 다음과 같은 일들은 처리할 수 없습니다.

1. Ajax는 클라이언트가 서버에 데이터를 요청하는 클라이언트 풀링 방식을 사용하므로, 서버 푸시 방식의 실시간 서비스는 만들 수 없습니다.

2. Ajax로는 바이너리 데이터를 보내거나 받을 수 없습니다.

3. Ajax 스크립트가 포함된 서버가 아닌 다른 서버로 Ajax 요청을 보낼 수는 없습니다.

4. 클라이언트의 PC로 Ajax 요청을 보낼 수는 없습니다.

## 📌 AJAX 요청 방식

### 1. XML Http Request 방식

- xmlhttprequest 객체를 이용한 정통적인 초창기 비동기 서버 요청 방식이다.
- 성능에는 문제는 없지만 코드가 복잡하고 가독성이 좋지 않다는 단점이 있었다. - Fetch나 axios 에 비해 비동기 콜백 구문이 복잡해질 수 있으며, 상대적으로 예외처리가 어렵다.
- 장점은 우리가 사용하는 대부분의 브라우저에 지원되며, XHR 객체의 다양한 속성을 이용할 수 있다.

```jsx
const xhr = new XMLHttpRequest()
xhr.open('GET', '/api/data')
xhr.onloa = function () {
  if (xhr.status === 200) {
    console.log(xhr.responseText)
  } else {
    console.log('요청 실패. 상태 코드 : ' + xhr.status)
  }
}
xhr.send()
```

### 2. fetch

- ES6에서 지원된 비동기 통신을 위한 자바스크립트 내장 API입니다. (내장 API 이므로 별도 import 없이 사용 가능)
- Promise 기반으로 동작하여 데이터를 다루기 편리하며 콜백지옥을 해결할 수 있습니다.
- 기본 응답 결과는 Response 객체로, json으로 바꾸거나 text로 바꾸는 별도의 처리 과정이 필요합니다.
- 구형 브라우저에서는 지원을 하지 않습니다.
- 네트워크 에러 발생 시 계속 기다려야합니다.
- API 요청을 취소할 수 없습니다.

```jsx
fetch('/api/data')
  .then((response) => {
    if (!response.ok) {
      throw new Error('응답 실패')
    }
  })
  .then((date) => {
    console.log(data)
  })
  .catch((error) => {
    console.log('에러 발생 :', error)
  })
```

### 3. axios

- 브라우저, Node.js를 위한 Promise API를 활용하는 HTTP 비동기 통신 라이브러리다. (Promise 기반)
- 크로스 브라우징 기반으로 브라우저 호환성이 뛰어나다.
- fetch에 존재하지 않는 기능이 많다. (자동으로 JSON 데이터 형식으로 변환, 요청 취소 및 타임아웃 설정 가능 등..)
- fetch와 달리 **요청과 응답의 취소와 중단이 가능**하며 XSRF 보호를 자동으로 지원한다. (XSRF는 Cross-SIte Request Forgery로, 웹사이트에서 발생할 수 있는 보안 취약점 중 하나로, 사용자가 의도치 않은 요청을 다른 쉡사이트로 전송하게끔 하는 공격이다.)
- 사용하려면 라이브러리 설치가 필요하다.

```jsx
axios
  .get('/api/data')
  .then((response) => {
    console.log(response.data)
  })
  .catch((error) => {
    console.log(error)
  })
```

참조  
https://tcpschool.com/ajax/ajax_intro_basic  
https://99geo.tistory.com/65  
https://aws.amazon.com/ko/what-is/ajax/  
https://ji-musclecode.tistory.com/65  
https://blog.naver.com/PostView.naver?blogId=tank100&logNo=223072221468
