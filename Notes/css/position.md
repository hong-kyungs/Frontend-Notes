# position

- `position` 프로퍼티는 요소의 위치를 정의한다. top, bottom, left, right 프로퍼티와 함께 사용하여 위치를 지정한다.
- CSS position 속성은 문서 상에 요소를 배치하는 방법을 지정한다. `static`, `relative`, `absolute`, `fixed`, `sticky` 속성을 값으로 갖는다.

## 1. static(기본위치)

- static은 position 프로퍼티의 기본값으로 position 프로퍼티를 지정하지 않았을 때와 같다.
- 기본적인 요소의 배치 순서에 따라 위에서 아래로, 왼쪽에서 오른쪽으로 순서에 따라 배치되며 부모 요소 내에 자식 요소로서 존재할 때는 **부모 요소의 위치를 기준으로 배치**된다.
- 기본적으로 이 값을 지정할 일은 없지만 이미 설정된 position을 무력화하기 위해 사용될 수 있다.
- 좌표 프로퍼티(top, bottom, left, right)를 같이 사용할 수 없으며 사용할 경우에는 무시된다.

<p align="center">
<img src="../../images/css/position-1.png" width="400">
</p>

## 2. relative(상대위치)

- 기본 위치(static으로 지정되었을 때의 위치)를 기준으로 좌표 프로퍼티(top, bottom, left, right)를 사용하여 위치를 이동시킨다. static을 선언한 요소와 relative를 선언한 요소의 차이점은 좌표 프로퍼티의 동작 여부뿐이며 그외는 동일하게 동작한다.
- 요소를 원래 위치에서 벗어나게 배치할 수 있게 된다. `top`, `bottom`, `left`, `right` 속성을 이용해서, 요소가 원래 위치에 있을 때의 상하좌우로 부터 얼마나 떨어지게 할지를 지정할 수 있다.

<p align="center">
<img src="../../images/css/position-2.png" width="400">
</p>

## 3. absolute(절대 위치)

- **부모 요소 또는 가장 가까이 있는 조상 요소(static 제외)를 기준으로 좌표 프로퍼티(top, bottom, left, right)만큼 이동한다. 즉, relative, absolute, fixed 프로퍼티가 선언되어 있는 부모 또는 조상 요소를 기준으로 위치가 결정된다.**
- **만일 부모 또는 조상 요소가 static인 경우, document body를 기준으로 하여 좌표 프로퍼티대로 위치하게 된다.** 따라서 부모 요소를 배치의 기준으로 삼기 위해서는 부모 요소에 relative를 정의하여야 한다.
- 이때 다른 요소가 먼저 위치를 점유하고 있어도 뒤로 밀리지 않고 덮어쓰게 된다. (이런 특성을 부유 또는 부유 객체라 한다)
- **absolute 선언 시, block 레벨 요소의 width는 inline 요소와 같이 content에 맞게 변화되므로 적절한 width를 지정하여야 한다.**

<p align="center">
<img src="../../images/css/position-3.png" width="400">
</p>

### 📍**relative 프로퍼티와 absolute 프로퍼티의 차이점**

- relative 프로퍼티는 기본 위치(static으로 지정되었을 때의 위치)를 기준으로 좌표 프로퍼티(top, bottom, left, right)을 사용하여 위치를 이동시킨다. 따라서 **무조건 부모를 기준으로 위치**하게 된다.
- absolute 프로퍼티는 부모에 static 이외의 position 프로퍼티가 지정되어 있을 경우에만 부모를 기준으로 위치하게 된다. 만일 부모, 조상이 모두 static 프로퍼티인 경우, document body를 기준으로 위치하게 된다. 따라서 absolute 프로퍼티 요소는 부모 요소의 영역을 벗어나 자유롭게 어디든지 위치할 수 있다.

<p align="center">
<img src="../../images/css/position-4.png" width="400">
</p>

## 4. fixed(고정위치)

- 부모 요소와 관계없이 브라우저의 viewport를 기준으로 좌표프로퍼티(top, bottom, left, right)을 사용하여 위치를 이동시킨다.
- **스크롤이 되더라도 화면에서 사라지지 않고 항상 같은 곳에 위치한다.**
- **fixed 프로퍼티 선언 시, block 요소의 width는 inline 요소와 같이 content에 맞게 변화되므로 적절한 width를 지정하여야 한다.**

<p align="center">
<img src="../../images/css/position-5.png" width="400">
</p>

## 5. sticky

- 스크롤하지 않을 때는 static position처럼 동작하다가 스크롤할 때는 이전 포스팅에서 배웠던 fixed position처럼 작동합니다.

<p align="center">
<img src="../../images/css/position-6.gif" width="400">
</p>

### **sticky position의 동작 방식**

1. 브라우저가 처음 랜더링 되었을 때 sticky 요소는 문서 흐름에 따라 일반적인 위치에 배치된다
2. 스크롤이 지정된 위치에 도달할 때까지 sticky 요소는 일반적인 흐름대로 따라 이동한다
3. 스크롤의 좌표가 지정된 위치에 도달하면 sticky 요소가 지정된 위치에 고정된다
4. 이제 지정된 위치 이하로 스크롤해도 해당 위치에 고정되어 유지된다.

참조  
https://poiemaweb.com/css3-position.
https://coding-factory.tistory.com/951
