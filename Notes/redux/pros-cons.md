# Redux의 장단점

### 장점

1. 단방향 모델링(**한가지 방향**으로만 바뀐다)임. action을 dispatch 할때마다 기록(history)이 남아 에러를 찾기 쉽다. 타임머신 기능을 사용할 수 있음

2. **상태의 중앙화** : **스토어(Store)**라는 이름의 전역 자바스크립트 변수를 통해 상태를 한 곳에서 관리하는데, 이를 **중앙화라 함. 전역 상태를 관리할때 굉장히 효과적**

3. Redux는 상태를 읽기 전용으로 취급한다. 상태가 읽기 전용이므로, **이전 상태로 돌아가기 위해서는 그저 이전 상태를 현재 상태에 덮어쓰기만 하면 됨.** 이런 식으로 실행 취소 기능을 구현.

### 단점

1. 아주 작은 기능이여도 리덕스로 구현하는 순간 몇 개의 파일(액션등을 미리 만들어놔야함)들을 필수로 만들어야하여 코드량이 늘어난다. - 코드작성이 '초기에는 복잡'하다. 스테이트 업데이트에 맞는 액션값들과 디스패치함수들 그리고 리듀서들... 등등 초기에 미리미리 전부 만들어 줘야하는 복잡성이 있다.
   → 단점을 보완하기위해 여러가지 라이브러리들이 출시되었다. 그중 `리덕스 툴킷`이 제일 유명하다.

2. 타임머신 기능을 사용하려면 불변성 개념을 지켜야 사용할 수 있으므로 매번 state라는 객체를 만들어줘야 함

3. Redux는 상태를 읽기 전용으로 취급할 뿐, 실제 읽기 전용으로 만들어주지는 않습니다. 때문에 상태를 실수로 직접 변경하지 않도록 항상 주의해야 합니다. 이를 예방하기 위해 `Immutable.js`같은 라이브러리도 존재합니다.

4. 다른 것 다 필요 없고 상태 관리를 중앙화하는 것만 있어도 된다면 **Context API** 를 사용

참조  
https://amyhyemi.tistory.com/103