## 1. 클라이언트 상태 관리

- SPAs 구조에서는 다양한 화면 렌더링이 필요하며, 상태기반으로 렌더링된다.
- 다양한 state 가 존재하며, 어떠한 state 는 서버와의 동기화 작업이 필요하다.

## 2. 리액트의 상태 관리

- Component Block State : 컴포넌트 내에서 가지고 있는 상태로, UI 는 이 state 기반으로 렌더링된다.
- COmponent Sharing State : 다른 node 계층에 전달하며, Props drilling 문제가 발생할 수 있다.

## 3. props drilling 을 해결하는 방법

- Context API 를 통한 해결
- Component Composition 을 통해 해결
  ```jsx
  export default function App() {
    const content = 'Who needs me?';
    return (
      <div className='App'>
        <FirstComponent>
          <SecondComponent>
            <ThirdComponent>
              <ComponentNeedingProps content={content} />
            </ThirdComponent>
          </SecondComponent>
        </FirstComponent>
      </div>
    );
  }
  ```

## 4. 상태 기반 컴포넌트 개발

- Events, Actions, States, Transitions 로 구성되며 이를 설계하는 과정이다
- Events
  - Click, mousedown, setTimeout, fetch 의 onload 와 같은 이벤트이다.
- Actions

  - 메세지 형태를 정의한다.
  - action 의 type 별 상태 변화를 정의했지만, actions 를 함수로 만들 수도 있다.
  - 결국 switch 문을 통해서 message 를 해석하고 상태를 변경하기 때문에.

  ```jsx
  const addData = (payload) => {"type":"increment", payload}
  fire(addData("lorem"));

  function reducer(state, action) {
    switch (action.type) {
      case 'increment':
        return { count: state.count + 1 };
      case 'decrement':
        return { count: state.count - 1 };
      default:
        throw new Error();
  }
  ```

- States
  - UI 변경에 영향을 미치게 되는 상태이다.
- Transitions
  - Reducer 와 같은 형태로 별도의 상태 변경 과정을 표현한다.
  - pure function 인지, testable 코드인지, view 에 독립적인지 확인해야한다.
