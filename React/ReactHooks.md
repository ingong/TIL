# React Hooks

## useReducer

### 사용법

`useReducer 사용법`

```jsx
// 초기 state를 두번째 파라미터로 전달(=initialArg)해 state를 초기화할 수 있다
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

`reducer 사용법`

```jsx
function reducer(state, action){
  // 새로운 상태를 만드는 로직
  // const nextState = ...
  return nextState;
}

// 혹은 아래처럼 간략하게 쓸 수도 있다
function reducer(state, action) => newStatae
```

### 설명

- 컴포넌트의 상태 업데이트 로직을 컴포넌트에서 분리가 가능하다.
- 명시적으로 정의한 메서드를 통해 상태 변경이 가능하다.
- 구체적인 상태 변경을 감추고, reducer에게 상태 변경 기능을 위임시킨다.
- 하위 컴포넌트에게 상태관리 변경 메서드를 전달하는 불편함을 해소시켜줄 수 있다. 대신 dispatch라는 매개체 역할의 함수를 전달해준다.
- reducer 가 순수함수의 형태이기 때문에 testable code 를 제공한다.
- 컴포넌트에서 관리하는 값이 여러개가 되어서 상태의 구조가 복잡해진다면 useReducer 로 관리하는 것이 더 편할 수도 있다.
  ex) 하나의 버튼 클릭으로 인해, 두 개의 상태를 변경시킬 때

### 키워드

상태 업데이트, 분리, reducer, 순수함수

### counter 예제

```jsx
const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
    </>
  );
}
```

[CodeSandbox Link](https://codesandbox.io/s/quirky-dream-7q0gx?file=/src/App.js)
