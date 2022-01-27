## 이터러블/이터레이터 프로토콜

### 이터러블

이터레이터를 리턴하는 `[Symbol.iterator]` 메서드를 가진 값이다.

Symbol 에 대한 설명은 이번 글에서 다룰 범위를 넘어가기 때문에 따로 학습하기를 추천한다. Symbol 에 대해서 간략하게 설명하면 ES2015 에서 추가된 JS 의 7번째 자료형으로, 변하지 않는 원시 자료형이다.

### 이터레이터

`{ value, done }` 객체를 리턴하는 next 메서드를 가진 값이다.

### 이터러블/이터레이터 프로토콜

**이터러블**을 `for ... of`, `전개 연산자` 등과 함께 동작하도록한 규약이다. 예를 들면 `for ... of` 을 순회할 때 이터레이터의 done 의 값이 false 일 때는 해당 value 를 반환하고, done 이 true 인 경우에는 해당 for ... of 문을 빠져나오게 하는 것도 해당 프로토콜로 인해 가능한 것이다.

이터러블과 이터레이터의 정의 그리고 이터러블/이터레이터 프로토콜에 기반해서 이터러블을 구현해보자. `3, 2, 1` 순으로 숫자를 출력하는 것을 목표로 작성해보자.

```jsx
const iterable = {
  [Symbol.iterator]() {
    let i = 3;
    return {
      next() {
        return i === 0 ? { done: true } : { value: i--, done: false };
      },
    };
  },
};

for (const a of iterable) console.log(a);
// 3, 2, 1
```

JS 의 배열을 순회할 수 있는 것도 JS 의 배열이 이터러블/이터레이터 프로토콜을 순회할 수 있기 때문에 가능한 것이다.

### JS 의 배열

```jsx
const arr = [1, 2, 3];
console.log(arr[Symbol.iterator]);
// ƒ values() { [native code] }
for (const a of arr) console.log(a);
// 1, 2, 3
```

위 예시처럼 `arr[Symbol.iterator]` 에 접근해보면 함수가 출력되고, 순회하면 결과값이 출력된다. `arr[Symbol.iterator]` 에 `null` 을 대입하면 어떻게 될까?

```jsx
const arr = [1, 2, 3];
arr[Symbol.iterator] = null;
for (const a of arr) console.log(a);
```

순회할 수 없다는 에러가 출력된다. `Set` 과 `Map` 객체도 동일하게 동작하는 것을 확인할 수 있었다.
