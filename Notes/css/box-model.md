# 박스 모델

모든 HTML 요소는 Box 형태의 영역을 가지고 있다. 이 Box는 콘텐트(Content), 패딩(Padding), 테두리(Border), 마진(Margin)로 구성된다.

<p align="center">
<img src="../../images/css/box-model-1.png" width="400">
</p>

브라우저는 박스 모델의 크기(dimension)와 프로퍼티(색, 배경, 모양 등), 위치를 근거로 하여 렌더링을 실행한다.

웹디자인은 콘텐츠를 담을 박스 모델을 정의하고 CSS 프로퍼티를 통해 스타일 (배경, 폰트와 텍스트 등)과 위치 및 정렬을 지정하는 것이라고 할 수 있다.

Box 모델을 구성하는 콘텐트(Content), 패딩(Padding), 테두리(Border), 마진(Margin)에 대한 설명은 아래와 같다.

| 명칭    | 설명                                                                                                                                                                                                    |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Content | 요소의 텍스트나 이미지 등의 실제 내용이 위치하는 영역이다. width, height 프로퍼티를 갖는다.                                                                                                             |
| Padding | 테두리(Border) 안쪽에 위치하는 요소의 내부 여백 영역이다. padding 프로퍼티 값은 패딩 영역의 두께를 의미하며 기본색은 투명(transparent)이다. 요소에 적용된 배경의 컬러, 이미지는 패딩 영역까지 적용된다. |
| Border  | 테두리 영역으로 border 프로퍼티 값은 테두리의 두께를 의미한다.                                                                                                                                          |
| Margin  | 테두리(Border) 바깥에 위치하는 요소의 외부 여백 영역이다. margin 프로퍼티 값은 마진 영역의 두께를 의미한다. 기본적으로 투명(transparent)하며 배경색을 지정할 수 없다.                                   |

## 📌 width / heigh 프로퍼티

width와 height 프로퍼티는 요소의 너비와 높이를 지정하기 위해 사용된다. 이때 지정되는 요소의 너비와 높이는 **콘텐츠 영역**을 대상으로 한다.

> 이는 box-sizing 프로퍼티에 기본값인 **content-box**가 적용되었기 때문이다. box-sizing 프로퍼티에 **border-box**를 적용하면 콘텐츠 영역, padding, border가 포함된 영역을 width / height 프로퍼티의 대상으로 지정할 수 있다.

만일 width와 height로 지정한 콘텐츠 영역보다 실제 콘텐츠가 크면 콘텐츠 영역을 넘치게 된다는 것에 유의하여야 한다.

## 📌 margin / padding 프로퍼티

margin 프로퍼티에 `auto` 키워드를 설정하면 해당 요소를 브라우저 중앙에 위치 시킬 수 있다.

## 📌 box-sizing 프로퍼티

`box-sizing` 프로퍼티는 width, height 프로퍼티의 대상 영역을 변경할 수 있다.

box-sizing 프로퍼티의 기본값은 content-box이다. 이는 width, height 프로퍼티의 대상 영역이 content 영역을 의미한다. box-sizing 프로퍼티의 값을 border-box로 지정하면 마진을 제외한 박스 모델 전체를 width, height 프로퍼티의 대상 영역으로 지정할 수 있어서 CSS Layout을 직관적으로 사용할 수 있게 한다.

| 키워드      | 설명                                                                              |
| ----------- | --------------------------------------------------------------------------------- |
| content-box | width, height 프로퍼티 값은 content 영역을 의미한다. (기본값)                     |
| border-box  | width, height 프로퍼티 값은 content 영역, padding, border가 포함된 값을 의미한다. |
|             |                                                                                   |

<p align="center">
<img src="../../images/css/box-model-2.png" width="400">
</p>

참조  
https://poiemaweb.com/css3-box-model
