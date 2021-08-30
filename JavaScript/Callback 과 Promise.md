## Callback 과 Promise

- 둘 다 자바스크립트에서 비동기 처리를 위해 사용되는 패턴입니다.
- Callback 은 함수의 처리 순서를 보장하기 위해 사용합니다. 하지만 함수를 중첩해서 사용하면 콜백지옥이 발생할 수 있고, 에러 핸들링이 어렵습니다.
- Promise 는 생성자 함수를 통해 인스턴스화하며, pending, resolve, reject 라는 3가지 상태를 갖습니다.
  - 진행 중일 때는 pending 상태입니다.
  - 성공 시, resolve 메서드를 호출해 후속 처리 메소드로 전달합니다.
  - 실패 시, reject 메서드를 호출해 후속 처리 메소드로 전달합니다.
- 후속 처리 메서드에는 then 과 catch 가 있으며, 둘 다 promise 를 반환합니다.
- then 을 가지고, 메서드 체이닝을 통해 콜벡지옥 문제를 해결할 수 있습니다.

```js
// Promise 객체의 생성
const promise = new Promise((resolve, reject) => {
  // 비동기 작업을 수행한다.

  if (/* 비동기 작업 수행 성공 */) {
    resolve('result');
  }
  else { /* 비동기 작업 수행 실패 */
    reject('failure reason');
  }
});
```
