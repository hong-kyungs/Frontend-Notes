# Component(컴포넌트)

## 📌 컴포넌트(Component)란?

- 리액트는 화면에서 UI 요소를 구분할 때 ‘컴포넌트’라는 단위를 사용한다. 리액트에서 앱을 이루는 가장 작은 조각, 부품이라고 할 수 있다.
- 컴포넌트를 만드는 것이 리액트의 본질이다! 여러 태그들을 하나의 독립된 부품으로 만들 수 있고, 그 부품을 이용하면 적은 복잡도로 소프트웨어를 만들 수 있고, 내가 만든 컴포넌트를 다른 사람에게 공유할 수 있고, 다른 사람이 만든 컴포넌트를 내가 사용할 수도 있다.→ 생산성을 끌어올리는 역할!
- 컴포넌트는 데이터(props)를 입력받아 View(state) 상태에 따라 DOM Node를 출력한다. 리액트는 컴포넌트안에 데이터와 화면을 하나로 묶어두고, state 부분, 즉 데이터가 바뀌면 render 부분을 통해 화면을 알아서 바꿔준다.
- 컴포넌트 이름은 항상 대문자로 시작하도록 한다.

## 📌 컴포넌트의 종류

리액트는 컴포넌트를 선언할 때, 크게 2가지 방법이 있다. 

1. **클래스 문법**
리액트의 기능 풀파워 사용가능하다. 하지만 class 문법을 알아야하고 좀 장황하다.
2. **함수 문법**
함수의 문법만 알면 사용가능하다. 하지만 기능이 부족했다.

    부족했던 기능 2가지?
    1. 컴포넌트 내부에 state를 만들어 사용하는 것.
    2. 컴포넌트의 생성, 변경, 소멸에 대한 이벤트인 life cycleAPI 사용

    
    ⇒ 최신 리액트에서 hook 개념이 도입되면서 부족했던 2가지 기능이 가능해졌다.
    그래서, 요즘은 **함수 문법을 선호**하지만, class 문법도 여전히 사용되고 있다. 
    

## 📌 class component(클래스 컴포넌트)

### 클래스 컴포넌트란?

- 클래스 컴포넌트는 자바스크립트 “클래스”기반 컴포넌트로, class로 정의하고 render( ) 함수에서 JSX 코드를 반환한다.

```jsx
class LikeButton extends React.Component {
      constructor(props) {
        super(props);
        this.state = { liked: false };
      }

      render() {
        if (this.state.liked) {
          return 'You liked this.'
        }

        return (
          <button onClick={() => this.setState({ liked: true })}>
            Like
          </button>
        );
      }
    }
```

### 클래스 컴포넌트 특징

1. render( ) 메서드 필수로 사용
    
    클래스 컴포넌트 안에 render() 메서드가 꼭 필요하고 메서드 안에 JSX 를 리턴한다. - render( )의 return 에 있는 부분이 화면에 그려진다.
    
2. this 키워드 사용하기
    
    state, props, refs,컴포넌트 메서드, 생명주기 메서드를 사용할 때 this 로 프로퍼티를 참조하여 사용한다.
    
3. return 문 안에 if문이나 for문을 쓸 수 없다 → 대신에 삼항연산자 or map 을 사용한다.

## 📌 function component(함수 컴포넌트)

### 함수 컴포넌트란?

- 말  그래도 자바스크립트의 “함수(function)” 기반 컴포넌트이다. 자바스크립트 함수를 선언하듯이 function으로 컴포넌트를 정의하고, return 문에 JSX 코드를 반환한다. 화살표 문법도 가능하다.
- 클래스 컴포넌트에 비해 코드가 간결하고, this를 쓸 일이 없다.

```jsx
function LikeButton() {
  const [liked, setLiked] = React.useState(false); //구조분해
  if (liked) {
    return 'You liked this.';
  }
  return (
    <button onClick={() => {
      setLiked(true);
    }}>Like</button>
  )
}
```

```jsx
const LikeButton = () => {
	const [liked, setLiked] = React.useState(false); //구조분해
  if (liked) {
    return 'You liked this.';
  }
  return (
    <button onClick={() => {
      setLiked(true);
    }}>Like</button>
  )
};
```

### 함수 컴포넌트를 사용하는 이유

1. Hooks

  과거에는 함수형 컴포넌트가 state, 라이프사이클을 지원하지 않았기 때문에 클래스형 컴포넌트를 많이 사용했지만, React v16 이후부터 **Hooks**를 통한 state 및 LifeCycle 관리가 가능해져 리액트에서 공식적으로 함수형 컴포넌트 사용을 권장한다. Hook의 useState를 사용해 state 를 관리할 수 있고, useEffect 를 사용해 LifeCycle 을 관리할 수 있어요.

2. 직관적인 코드

  자바스크립트의 함수(function) 선언, 화살표 함수를 그대로 사용해 컴포넌트를 사용 가능하기 때문에 개발자에게 직관적이다.

3. 메모리 자원 효율

  클래스형 컴포넌트에 비해 함수형 컴포넌트가 비교적 메모리 자원을 적게 사용한다.

참조  
생활코딩  
제로초
https://life-with-coding.tistory.com/508  