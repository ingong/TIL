## Well-formed iterator

잘 구현된 `iterator` 은 2가지 특징을 가지고 있다. 첫 번째는 `iterable` 로 순회할 수 있을 뿐만 아니라, `iterator` 를 for ... of 문에 넣었을 때도 모든 값을 순회하도록 되어있다. 두 번째는 `iterator` 를 `next` 메서드로 진행 한 후에도 순회할 수 있다. 첫 번째 예시부터 살펴보자.

```jsx
const arr = [1, 2, 3];
let iter = arr[Symbol.iterator]();
for (const a of iter) console.log(a);
// 1, 2, 3
```

두 번째 예시를 살펴보자.

```jsx
const arr = [1, 2, 3];
let iter = arr[Symbol.iterator]();
iter.next();
for (const a of iter) console.log(a);
// 2, 3
```

이전에 우리가 구현했던 iterable 객체도 동일하게 동작하는지 살펴보자.

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
const iterator = iterable[Symbol.iterator]();

for (const a of iterator) console.log(a);
```

안타깝게도 우리가 구현한 `iterable` 이 반환한 `iterator` 는 `iterable` 하지 않다고 출력된다. 무엇이 문제일까? iterator 가 순회되기 위해서는 `Symbol.iterator` 메서드를 가져야하기 때문이다.

이를 위해서는 `iterator` 가 `Symbol.iterator` \*\*\*\*메서드를 갖도록 추가해주고, this 로 본인을 반환하도록 작성해줘야한다. 즉, 본인도 next 메서드를 갖는 `iterator` 인 동시에 `Symbol.iterator` 메서드를 갖는 `iterable` 이 되어야 한다.

```jsx
const iterable = {
  [Symbol.iterator]() {
    let i = 3;
    return {
      next() {
        return i === 0 ? { done: true } : { value: i--, done: false };
      },
      [Symbol.iterator]() {
        return this;
      },
    };
  },
};
const iterator = iterable[Symbol.iterator]();

for (const a of iterator) console.log(a);
```

이렇게 iterable 의 `Symbol.iterator` 메서드가 반환하는 `iterator` \***\*가 자기 자신을 반환하는 `Symbol.iterator` 메서드를 가지고 있을 때 이를 `well-formed iterable` \*\***이라고 부른다.

`well-formed iterator` 을 정리하면 다음과 같다.

- `iterator` 의 `Symbol.iterator` 실행 결과가 자기 자신이다.
- `iterable` 과 `iterator` 모두 `for ... of` \*\*\*\*로 순회할 수 있다.
- `iterator` 을 일정 부분 순회한 후에 다시 순회를 해도 순회가 가능하다.

두 번째 특징은 함수 내부의 실행 흐름을 제어할 수 있다는 generator 의 핵심원리와 연관이 있다.

## 이터러블/이터레이터 프로토콜은 어디까지

지금까지는 `**Array, Set, Map`\*\* 에 대해서만 살펴봤지만 사실 이터러블/이터레이터 프로토콜은 우리가 편하게 사용하는 대부분의 오픈소스라이브러리나 DOM APIs 에도 구현이 되어있다. 한 가지 예시를 알아보자.

```jsx
const all = documnet.querySelectorAll('*');
let iterator = all[Symbol.iterator]();
cnsole.log(all);
// NodeList(9)
// [html, head, meta, meta, meta, title, script, body, div#root]

for (const a of iterator) console.log(a);
// 순회가 가능하다!
```

우리가 JavaScript 로 DOM 에 접근할 때 사용했던 `document.querySelectorAll` 의 반환값도 `NodeList` 다. 즉, 배열을 순회한다는 표현보다는 앞으로도 이터러블/이터레이터 프로토콜을 만족하도록 내부적으로 구현되어 있다는 표현이 더 맞는 표현인 것이다. `immutbale js` \*\*\*\*에서도 객체를 `for ... of` 문으로 순회할 수 있도록 `Symbol.iterator` 메서드가 구현되어 있다. 지금까지 당연스럽게 순회했던 객체들이 어떻게 내부적으로 순회가능을 구현했는지 알게 된 학습이였다.
