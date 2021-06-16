### Ecma 인터내셔널 (Ecma International)

Ecma 인터내셔널은 정보 통신에 대한 표준을 제정하는 비영리 표준화 기구이다.

이 기구가 정의한 표준들은 다음과 같다.

ex) C# 언어 규격, CD 롬 볼륨과 파일구조, JSON 포맷 등

각각의 표준은 번호를 가지고 있으며 JS 에 관련해서 우리가 알아야 하는 표준은 ECMA-262 이다.

### ECMA-262

ECMA-262 는 범용 목적의 스크립트 언어에 대한 명세를 담고 있다.

그렇다면 스크립트 언어는 어떻게 정의할 수 있을까? 스크립트 언어에 대한 정의를 알아보자

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dfce70c2-47ea-40f7-855c-ac527180f2c3/Untitled.png)

### 스크립트 언어

스크립트 언어는 독립된 시스템에서 작동하도록 설계된 프로그래밍 언어이다.

즉, 독립된 시스템에서 작동되기 위한 언어이다.

> 스크립트 언어에 포함되는 프로그래밍 언어들은 독립된 시스템을 위해 존재합니다. 예를 들어, *이동하기, 달리기, 점프하기*라는 명령어를 여러분들이 사용할 수 있다고 생각해봅시다. 그렇다면 사람이나 개, 아니면 게임 캐릭터처럼 여러분들의 명령을 입력받고, 실행할 수 있는 무언가가 있어야 하겠죠? 만약 *이동하고, 달리고, 점프*를 할 수 있는 것들이 없다면 명령어는 아무 쓸모가 없겠죠. - Michael Aranda 의 What’s the difference between JavaScript and ECMAScript 글 번역본

여기서 찾을 수 있는 스크립트 언어의 특징으로는 응용 프로그램과 독립적이며, 사용자가 직접 프로그램을 의도에 따라 동작시킬 수 있다는 것이다. 스크립트 언어를 이용한 명령어의 실행이 시스템 내부에서 어떤 원리로 동작하는지는 전혀 상관하지 않는다. JS 가 브라우저에서 동작할 때, 브라우저의 내부 동작 원리와의 무관하게 동작하는 원리를 하나의 예시로 들 수 있다.

### ECMAScript

`ECMAScript` 는 ECMA-262 기술 규격에 의해 정의된 범용 스크립트 언어이다. 동의어로는 EMCAScript 사양 (ECMAScript specification) 이 있다. 우리가 ECMA 스펙이라고 했던 개념도 결국 `ECMAScript` 를 이야기하는 것이였다.

`ECMAScript` 는 ECMA-262 에서 정의된 하나의 사양을 의미한다. `ECMAScript`는 스크립트 언어가 준수해야 하는 규칙, 세부 사항 및 지침을 제공한다.

> 이해가 어렵다면 좀 더 쉬운 예시를 들어보죠. 우리가 일상생활에서 쓰는 언어의 기준이 되는 국어를 *표준어*라고 부르고, *국립국어원*에서 관리하고 있습니다. 그리고 표준어는 국립국어원에서 제정한 *여러가지 규칙들*(대표적으로 발음이나 맞춤법)을 일정한 원리를 따르고 있습니다.

- Michael Aranda 의 What’s the difference between JavaScript and ECMAScript 글 번역본
  >

ECMAScript에서도 마찬가지이다. 국립국어원은 Ecma 인터내셔널, ECMA-262는 표준어고, ECMAScript는 맞춤법과 같은 규칙으로 생각한다면 보다 쉽게 이해할 수 있다. 즉, ECMA-262 이라는 표준어(기술규격)가 업데이트 될 때마다, 맞춤법에 비유되는 ECMAScript 도 그 규격에 맞게 업데이트되는 것이다.

### JavaScript

JS 는 ECMAScript 스펙을 준수하는 범용 스크립트 언어이다. 또한 JS 는 ECMA 스펙에 포함되지 않는 확장 기능을 제공한다. 만약 ECMAScript 문서를 읽는다면 **어떻게 스크립트 언어를 만들 수 있는지**를 알 수 있다. 반면 JavaScript 문서를 읽게 된다면, **어떻게 스크립트 언어를 쓸 수 있는지**를 알 수 있다.

### ECMAScript 6

ECMAScript 6 는 ECMA-262 표준의 제 6 판이며, ECMAScript 사양의 주요 변경 사항 및 개선 사항을 명시한다. 동의어로는 ‘ES6’, ‘ES2015’, ‘ECMAScript 2015’가 있다.

국립국어원에서는 필요에 따라 표준어 규칙을 바꾸거나 새로운 단어를 표준어에 추가하기도 한다. Ecma 역시 마찬가지로, 필요성에 따라 ECMAScript를 개정한다.

ex) let & const, arrow functions, default parameters, destructuring, object initialize, template literals, class, promise, spread, rest parameter, Set & Map, import/export 키워드로 외부 모듈의 함수/변수 사용 가능
