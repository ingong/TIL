## 옵저버 패턴은 왜 사용할까?

Subject (이벤트 발행자) 는 관찰자의 참조를 보유할 필요가 없으며,

단지 데이터가 변화했을 때 호출할 핸들러만 전달하면 되기 때문이다.

## 옵저버 패턴이란 무엇인가?

옵저버 패턴은 `Subject` 와 `Observer` 로 구성된다.

`Subject` 는 변화를 만드는 주체이다. `Observer` 는 이 변화 이후에 특정한 `Action` 을 행해야하는 주체이다.

그렇다면 `Observer` 들은 어떻게 이 변화를 감지할까?

크게 2가지 방법이 있다. push or pull mechanism 이다.

pull mechanism 에서 `observer` 들은 지속적으로 `Subject` 에게 변화가 발생했는지 확인한다.

push mechanism \*\*\*\*은 `Subject` 가 `Observer` 에게 변화를 알리는 방식이다.

push mechanism \*\*\*\*은 pull mechanism 에 비해 더욱 선호되는 방식이다.

```jsx
const createStore = () => {
  let state;
  const listeners = [];
  const getState = () => state;
  const subscribe = fn => listeners.push(fn);

  const changeState = () => {
    listeners.forEach(v => v());
  };

  return {
    subscribe,
    changeState,
    getState,
  };
};

const observer1 = {
  changeOccur() {
    console.log('observer1 에서 변화감지');
  },
};

const store = createStore();

store.subscribe(observer1.changeOccur);
store.changeState();
```
