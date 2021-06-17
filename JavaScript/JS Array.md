### JS 의 배열은 배열이 아니다?

일반적으로 배열이라는 자료 구조는 메모리 공간이 빈틈없이 연속적으로 나열된 자료 구조이다. 즉, 배열의 요소는 **하나의 타입**으로 통일되어 있으며, 서로 연속적으로 인접해있다. 이러한 배열을 **밀집 배열**(dense array) 라 한다.

이처럼 배열의 요소는 동일한 크기를 갖으며 빈틈없이 연속적으로 이어져 있으므로 아래와 같이 인덱스를 통해 단 한번의 연산으로 임의의 요소에 접근(임의 접근(random access), 시간 복잡도 O(1))할 수 있다. 이는 매우 효율적이며 고속으로 동작한다.

하지만 배열에 요소를 삽입하거나 삭제하는 경우, 배열 요소를 연속적으로 유지하기 위해 요소를 이동시켜야한다.

JS 의 배열은 배열의 요소를 위한 각각의 메모리 공간이 동일한 크기를 갖지 않아도 되며, 연속적으로 이어져있지 않을 수도 있다. 배열의 요소가 연속적으로 이어져 있지 않은 배열을 **희소 배열(sparse array)**이라 한다.

이처럼 JS 의 배열은 엄밀히 말해 일반적 의미의 배열이 아니며, 일반적인 배열의 동작을 흉내낸 특수 객체이다.

```jsx
console.log(Object.getOwnPropertyDescriptors([1, 2, 3]));
/*
{
  '0': { value: 1, writable: true, enumerable: true, configurable: true },
  '1': { value: 2, writable: true, enumerable: true, configurable: true },
  '2': { value: 3, writable: true, enumerable: true, configurable: true },
  length: { value: 3, writable: true, enumerable: false, configurable: false }
}
*/
```

이처럼 자바스크립트 배열은 인덱스를 프로퍼티 키로 갖으며 length 프로퍼티를 갖는 특수한 객체이다. 자바스크립트 배열의 요소는 사실 프로퍼티 값이다. 자바스크립트에서 사용할 수 있는 모든 값은 객체의 프로퍼티 값이 될 수 있으므로 어떤 타입의 값이라도 배열의 요소가 될 수 있다.

일반적인 배열과 자바스크립트 배열의 장단점을 정리해보면 아래와 같다.

- 일반적인 배열은 인덱스로 배열 요소에 빠르게 접근할 수 있다. 하지만 특정 요소를 탐색하거나 요소를 삽입 또는 삭제하는 경우에는 효율적이지 않다.
- 자바스크립트 배열은 `해시 테이블`로 구현된 객체이므로 인덱스로 배열 요소에 접근하는 경우, **일반적인 배열보다 성능적인 면에서 느릴 수 밖에 없는 구조적인 단점**을 갖는다. 하지만 특**정 요소를 요소를 삽입 또는 삭제하는 경우에는 일반적인 배열보다 빠른 성능을 기대**할 수 있다.

이처럼 인덱스로 배열 요소에 접근할 때 일반적인 배열보다 느릴 수 밖에 없는 구조적인 단점을 보완하기 위해 대부분의 모던 자바스크립트 엔진은 배열을 일반 객체와 구별하여 보다 배열처럼 동작하도록 최적화하여 구현하였다.

```jsx
const arr = [];
console.time('Array Performance Test');
for (let i = 0; i < 10000000; i++) {
  arr[i] = i;
}
console.timeEnd('Array Performance Test');
// 약 340ms

const obj = {};
console.time('Object Performance Test');
for (let i = 0; i < 10000000; i++) {
  obj[i] = i;
}
console.timeEnd('Object Performance Test');
// 약 600ms
```
