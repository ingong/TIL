## 1. 비동기 프로그래밍

- JavaScript는 단일 스레드 언어입니다. 작업이 시간이 많이 걸리는 경우 단일 스레드를 차단할 수 있으며 이러한 블록으로 인해 성능 문제가 발생할 수 있습니다. 브라우저 내의 기본 스레드 블록은 느리거나 응답하지 않는 사용자 인터페이스로 나타날 수 있습니다.
- 비동기 프로그래밍에서는 이를 해결하기 위해 메인 스레드에서 외부로 작업을 전달하고, 다른 스레드에서 이 작업을 수행합니다.(**비동기 호출**).
- 이를 통패 메인 자바 스크립트 스레드를 차단하지 않고 자바 스크립트 파일을 계속 실행할 수 있습니다. 다른 곳에서 실행하기 위해 작업을 전달할 때 비동기 프로그래밍에서 우리는 종종 결과가 미래의 어느 시점에서 반환 될 때 실행할 함수를 제공합니다.
- 비동기 코드는 코드가 실행되고 반환 될 수있는 다른 순서를 알아야하므로 작성하기 어려울 수 있습니다. 따라서 callback, promise 패턴을 통해서 코드의 실행 순서를 직관적으로 확인할 수 있게 합니다.

## 2. Callback 과 Promise

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

## 3. Async 와 Await

- Promise를 더욱 쉽게 사용할 수 있도록 ES2017 문법입니다. 함수의 앞부분에 async 키워드를 추가하고, 함수 내부에서 Promise의 앞부분에 await 키워드를 사용합니다.
- 이를 통해 동기적인 코드 흐름으로 개발이 가능하며, 개발자는 try catch 를 통해 에러 핸들링을 해야합니다.

## 4. JS 의 자료형

- 원시타입
  - boolean, string, number, undefined , null , symbol 이 있습니다. undefined 는 선언만 되어있고 값은 없는 상태이며, null 은 자료형이 객체이며 빈 값을 의미합니다.
  - 실제 저장된 값의 메모리 주소가 변수에 할당
  - Number Type
    다른언어에는 int double 등 숫자타입의 다양함이 있지만, number는 하나만 있습니다. JS 는 정수만을 위한 타입이 없고, 모든 수를 실수로 처리합니다.
- 객체타입
  - 객체 타입을 변수에 할당하면, 변수에는 실제 객체가 저장된 힙 메모리 주소가 저장

## 5. 실행컨텍스트 (Execution Context)

- ECMAScript 스펙에 따르면, **실행 가능한 코드**를 형상화하고 구분하는 추상적인 개념입니다.
- 자바스크립트 엔진에 의해 만들어지고 사용되는 코드 정보를 담은 객체의 집합
- 쉽게 설명하면, **실행 가능한 코드가 실행되기 위해 필요한 환경입니다.**
- 실행 컨텍스트의 3가지 객체로 Variable Environment Object, Lexical Environment Object, thisValue 를 가집니다.
  - **Variable Environment Object (변수 환경 객체)**

    - 실행에 필요한 여러 정보를 담는 객체 (변수 객체)
    - 내부에서 선언된 변수(Variables), 함수 선언(Function Declarations), 함수 매게 변수(Formal Parameters)들을 저장
    - 새로운 변수나 함수가 등장하더라도 절대 변하지 않음

  - **Lexical Environment Object (렉시컬 환경 객체)**

    - 식별자와 값을 관리하고, 외부 상위 스코프에 대한 참조를 기록하는 데 사용하는 자료구조

  - **this Binding**

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4ce2b068-700d-47f6-8990-281331ad6849/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211103%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211103T113355Z&X-Amz-Expires=86400&X-Amz-Signature=5515392b18e9f411e876d08eacb05737a0f295c9aefde3cc3476473e19deb425&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
