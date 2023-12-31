# setState & useState 사용하는 이유

## state 변경시, 왜 직접 바꾸지 않고 setState, useState를 사용해야할까?

state는 컴포넌트 렌더링에 영향을 주는 데이터를 갖고 있는 객체인데, 이것을 업데이트 하기위해서는 setState, useState가 필요하다. 직접 state를 수정하면 리액트는 render 함수를 호출하지 않아서 렌더링이 일어나지 않고 setState를 호출하여 state를 변경하면 리액트 엔진이 render 함수를 이용해서 렌더링을 실행하기 때문입니다.

⇒ **state의 값이 변경되면 state를 관리하는 컴포넌트의 render함수가 다시 호출**된다. 즉 **props나 state의 값이 바뀌면 화면이 다시 그려진다.**

값이 변경 되었다는 것을 판단하기 위해 리액트는 저장된 state를 비교 연산하는데, 이 때 객체이기 때문에 비교하는 판단 근거가 객체의 메모리 주소임으로 직접 state 값을 수정 할 경우 변경이 안된 것으로 판단하고 상태 변경이 일어나도 렌더링이 일어나지 않을 수 있다.

**state는 꼭 불변성을 유지하도록 직접 수정하지 말아야 한다!**
