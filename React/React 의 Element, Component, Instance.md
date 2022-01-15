## 이전의 UI 라이브러리

클래스형 컴포넌트는 Class 의 형태로 리액트 컴포넌트를 정의하고, 이를 인스턴스화해서 화면에 컴포넌트를 렌더링한다. 리액트의 컴포넌트에 대한 개념을 학습하던 중 기존의 UI 라이브러리는 부모 컴포넌트가 자식 컴포넌트와 본인이 가지고 있는 `DOM Node` 도 관리해야했다. `DOM Node` 라는 단어가 궁금해졌다. `DOM Node` 는 무엇일까?

### DOM Node 란 무엇일까?

먼저 `DOM` 의 정의부터 알아보자. DOM 에 대한 위키피디아의 정의는 **HTML, XML 문서의 프로그래밍 인터페이스다**. DOM 은 HTML 문서를 태그 트리 구조로 표현한다. 여기서 인터페이스란 물리적 매개체 정도로 이해하면 좋을 것 같다.

노드란 어떤 객체의 구성 요소 또는 문서에 관한 정보를 담고 있는 계층적 정보 단위이다. 즉, `DOM Node` 란 **DOM 에 대한 정보를 담고 있는 구성요소**로 이해하면 좋을 것 같다.

리액트는 자식 컴포넌트와 본인이 가지고 있는 DOM Node 를 관리해야했고, 자식과의 강한 결합도를 가지고 있는 것은 문제가 될 수 있었다. 왜 문제가 됐을까? 결합도가 낮은 경우의 장점에 대해서 알아보면 이해가 빠를 것 같다. 결합도가 낮은 경우 각 요소들이 업무를 독립적으로 수행하고, 요소들이 자율적으로 유지되며, 하나의 요소를 변경할 때 다른 요소를 변경할 필요가 없어진다. 결합도가 높다면, 하나의 요소의 변경이 다른 요소에도 영향을 미칠 수 있고, 이는 예측을 어렵게하고 유지보수를 어렵게 하지 않을까라는 생각이다.

## 리액트는 어떻게 해결했을까?

리액트는 이 강한 결합도를 `Elements` 를 통해 해결했다. `Elements` 란 컴포넌트를 JSON 으로 표현한 것이며, 컴포넌트의 type, properties, children 에 대한 정보를 가지고 있다. JSON 이란 key-value 쌍으로 이루어진 데이터를 전송하기 위한 데이터 포맷을 의미한다. React 는 아래와 같은 DOM 을 다음과 같이 JSON 의 형태로 해석한다.

```jsx
<button class="button">
  <b>OK!</b>
</button>
```

```jsx
{
	type : 'button',
	props : {
		className: 'button',
		children {
			type: 'b',
			children: 'OK!',
		}
	}
}
```

다음과 같은 버튼이 있다고 가정해봅시다.

```jsx
const DangerButton = ({ children }) => ({
  type: Button,
  props: {
    color: 'red',
    children: children,
  },
});
```

DangerButton 은 Button 이 DOM Node 인지, Class 인지, Function 인지 신경 쓸 필요가 없다. 그냥 Button 엘리먼트에 `props` 를 `input` 으로 주입하고 있을 뿐이다.

즉, `React` 의 `Element` 는 `DOM Node` 나 리액트 컴포넌트에 대한 `JSON 요약본이다.`

이렇게 각각의 컴포넌트에 대한 정보를 Elements 의 형태로 나타내고 합침으로써 리액트는 부모 자식 관계를 느슨하게 형성할 수 있다.

한 가지 예시를 더 다뤄보겠다. 다음을 호출했다고 가정해보자.

```jsx
ReactDOM.render(
  {
    type: Form,
    props: {
      isSubmitted: false,
      buttonText: 'OK!',
    },
  },
  document.getElementById('root')
);
```

리액트는 input 으로 사용될 props 를 토대로 Form Component 에게 어떤 `Element Tree` 를 return 하는지 물어본다. 그리고 단순한 원시 요소 측면에서 `Element Tree` 에 대한 이해를 점진적으로 정리한다.

```jsx
// React: You told me this...
{
  type: Form,
  props: {
    isSubmitted: false,
    buttonText: 'OK!'
  }
}
// React: ...And Form told me this...
{
  type: Button,
  props: {
    children: 'OK!',
    color: 'blue'
  }
}
// React: ...and Button told me this! I guess I'm done.
{
  type: 'button',
  props: {
    className: 'button button-blue',
    children: {
      type: 'b',
      props: {
        children: 'OK!'
      }
    }
  }
}
```

이 과정이 끝난 이후에 리액트는 DOM 트리에 대한 정보를 알게 되고, ReactDOM 이나 React Native 는 DOM Node 에 필수적인 변화만 부여해서 업데이트한다. 이 점진적인 Refine 과정은 React 가 더욱 최적화를 쉽게 하게 한다. 또한 리액트와 불변성은 함께 동작하여 더욱 최적화를 빠르게 이뤄낸다.

인스턴스는 클래스로 선언된 컴포넌트가 가지는 것이며, 직접 만들어낼 필요가 없다. 리액트는 모든 클래스 컴포넌트에 대한 인스턴스를 생성하며, 메서드와 로컬 상태를 활용하여 객체 지향적으로 프로그래밍할 수 있다.

마지막으로 정리하자면, `element` 란 DOM Node 또는 컴포넌트에 대한 정보를 JSON 의 형태로 나타낸 것이다. `Component` 란 `props` 를 `input` 을 받아서 `element tree` 를 반환하는 함수 또는 클래스이다.
