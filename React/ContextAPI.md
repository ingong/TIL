### 요약

```jsx
# Context API 는 왜 사용하는가?
다양한 네스팅된 컴포넌트들에게 데이터를 전달하기 위해서 사용.
Props Drilling 문제를 해결할 수 있다.

# Context API 의 한계는 무엇인가?
해당 컴포넌트를 재사용할 수 없다.
전역 상태의 일부를 사용하는 컴포넌트에서는 다른 상태가 변경되어도 리렌더링이 발생한다.

# Context API 는 어떻게 사용하는가?
createContext 로 Context 객체를 만든다.
Provider 를 정의하고, 상태를 구독할 컴포넌트들의 상위에 감싼다. Provider 는 상태의 변화를 알린다.
함수형 컴포넌트 useContext 를 통해 상태를 구독해서 사용한다.
클래스 컴포넌트의 경우 ContextType 을 사용할 수 있다.
Context.Consumer 로 사용할 수도 있다.

# 이에 대한 대안은 무엇인가?
Recoil 을 사용할 수 있다.
```

# Context API

리액트는 기본적으로 부모에게 자식에게 데이터를 props 를 통해 전달되지만, 여러 컴포넌트들에게 전해줘야하는 props 의 경우 이 과정이 번거로울 수 있다. context 를 이용하면 트리 단계에서 명시적으로 props 를 넘겨주지 않아도 값을 공유할 수 있다.

### `Context 사용하기 전에 고려할 것`

Context 의 주된 용도는 다양한 레벨에 네스팅된 많은 컴포넌트들에게 데이터를 전달하는 것이다. context 를 사용하게 되면 컴포넌트를 재사용하는 것이 어려워진다. 여러 레벨에 걸쳐 props 를 넘기는걸 대체하는 데에 context 보다 컴포넌트 합성이 더 간단할 수 있다. 컴포넌트의 합성에 대해서는 다음에 좀 더 자세히 알아보도록한다.

### `React.createContext`

Context 객체를 만드는 API 이다. Context 객체를 구독하고 있는 컴포넌트를 렌더링할 때는 React 는 트리 상위에서 가장 가까이 짝이 맞는 `Provider` 로부터 현재값을 읽어온다.

```jsx
import React from 'react';

const context = React.createContext({
		text: ''
	});

export context
```

### `Context.Provider`

Context 오브젝트에 포함된 React 컴포넌트인 Provider 는 context 를 구독하는 컴포넌트들에게 context 의 변화를 알리는 역할을 한다. Provider 컴포넌트는 `value` prop 을 받아서 하위 컴포넌트들에게 전달한다. 여러 Provider 를 배치하는 것도 가능하며, 이 경우 하위 Provider 의 값이 우선시된다.

Provider 하위에서 해당 context 를 구독하는 모든 컴포넌트는 Provider 의 value prop 이 바뀔 때마다 다시 렌더링된다.

### `Context.Consumer`

context 의 변화를 구독하는 React 컴포넌트이다. 이 컴포넌트를 사용하면 함수 컴포넌트에서 context 를 구독할 수 있으며, Context.Consumer 의 자식은 함수를 반환해야한다.

### `useContext`

컴포넌트를 중첩하지 않고도 `**React context**` 를 구독할 수 있게 해준다. 이 방법은 함수형 컴포넌트에서만 사용이 가능하다.

### `contextType`

클래스 컴포넌트의 경우에는 `contextType` 을 사용해서 Context 내에 저장되어 있는 전역 데이터에 접근할 수 있다.

Context API 는 공유 상태를 원하는 컴포넌트에서 적절히 사용할 수 있고 이는 Props Drilling 에 대한 문제를 해결해줬다. 하지만 모든 기술이 모든 문제를 완벽하게 해결하지 못한 것처럼 Context API 도 그러하다. Context API 가 갖고 있는 문제는 다음과 같다. `생성한 Context 의 일부 상태만 구독하고 있는 컴포넌트일지라도 Contexst 의 다른 상태가 변경되면 리렌더링이 된다.` 이는 Context 를 여러 개 생성함으로써 해결이 가능하다.

Context API 와 유사한 기능을 제공하는 Recoil 로도 이 문제를 해결할 수 있다. Context 에서는 구독한 하위 컴포넌트들이 모두 리렌더링이 되지만, Recoil 은 atom, selector 를 구독하면 구독한 컴포넌트에서만 리렌더링이 발생한다.

[The Problem with React's Context API](https://leewarrick.com/blog/the-problem-with-context/)

[Context.Consumer vs useContext() to access values passed by Context.Provider](https://stackoverflow.com/questions/56816374/context-consumer-vs-usecontext-to-access-values-passed-by-context-provider)
