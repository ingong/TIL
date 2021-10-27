## Memorize

- **The goal of the Internet Architecture** MCCCLAND
- Protocol
  Message format, order, Local action
- Architectural Assumptions
  인터넷은 네트워크의 네트워크 / 게이트웨이는 연결 상태를 유지하지 않는다 / **라우팅 복잡성은 게이트웨이에 있어야한다 /** 시스템은 광범위한 네트워크의 변화를 수용할 수 있어야한다.

## Internet

### 정의

네트워크간의 네트워크를 의미한다.

컴퓨터로 연결하여, TCP/IP 라는 프로토콜을 이용해 정보를 주고 받는 컴퓨터 네트워크다.

### 왜 Internet 이 필요한가? 인터넷은 이를 어떻게 해결?

인터넷은 네트워크간 서로 호환되지 않을 수 있는 문제를 해결한다.

비호환성을 해결하기 위해서는 네트워크 기술간 translator 를 적용하는 방법이 있다. 하지만 이는 N2 의 시간 복잡도를 필요로하는 비용이 많이 드는 작업이다.

두 번째 방법은 공통의 미들웨어를 만드는 것이다. 인터넷에 연결하고자하는 모든 네트워크 기술은 공통의 캡슐화로 데이터를 운반한다. 이러한 일반적인 캡슐화를 IP 라고 한다.

### Internetworking

src, data, router, dst

tracert 를 통해 페킷의 전송 경로를 추적할 수 있다.

## protocol

**Data Communication Components 5가지**

⇒ Sender, Message, Transmission Medium, Receiver, Protocol

### **protocol**

프로토콜은 송수신자가 사용할 규칙을 정의하며, 모든 중간 장치는 효율적인 의사소통 또는 특정 목적을 달성을 위해 이를 지켜야한다.

`3가지 측면`을 반드시 준수해야한다.

`3가지 측면`을 반드시 준수해야한다.

1. Message Format
2. Order of Message
3. Local action (해당 메시지를 받은 이후에 해야하는 행동)

### protocol layering (프로토콜 계층화)

- 많은 네트워크 프로토콜은 계층구조를 이루고 있다. 복잡한 테스크를 단순하고, 작게 나눈다.
- 하위 계층 프로토콜을 사용하여 프로토콜의 사양 밖의 세부 사항을 처리

**Advantages**

- 상호 독립적인 모듈화가 가능하다.
- 프로토콜 내부는 블랙박스로 정의 될 수 있다.

**Disadvantages**

- 간단한 작업도 복잡해질 수 있다. 사용하지 않아도 되는 계층도 거쳐야한다.

**Principles**

- 양방향 통신을 원한다면, 각각은 서로 다른 tasks 를 수행할 수 있어야한다.
- 두 사이트의 각 레이어에 있는 두 객체는 동일해야한다.

## The goal of the Internet Architecture ⇒ MCCCLAND

### **primary goal**

develop an effective technique for `multiplexed utilization` of existing interconnected networks

### **second-level goal**

1. Internet communication `must continue despite loss` of networks or gateways.

   1. **Packet switching vs circuit switching**

      ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/65870326-5f7e-44b9-90ff-6a45bf6fcf46/Untitled.png)

   b. **Fate Sharing, End-to-End Principle**

   - Fate Sharing
     통신 끝점과 **동일한 위치**에 활성 **통신 연결을 유지하는 데 필요한 모든 상태** 배치
   - End-to-End Principle
     모든 복잡한 기능은 엔드 호스트에만 배치된다.
     새로운 어플리케이션의 도입이 용이함

2. Internet Architecture must support `multiple types of communication services`
3. Accomodate `a variety of networks`

   1. The Curse of Narrow Waist

      ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b722d2fb-3173-404b-bee0-0ac18956aaaf/Untitled.png)

   IP 에 대해서 변화를 주는 것이 어렵다.

4. Permit `distributed management` of its resources
5. `Cost-effective`
6. Host Attachemnt `with a low level of effort`

   IP is "plug and play"

   IP stack 과 관련된 모든 것은 인터넷과의 연결이 가능하다.

   하지만 이 각각의 시스템과 프로그래머에게 부하가 가중될 수 있다.

7. The resources used in the internet architecture must be `accountable`

   비용관련된 이슈

## Architectural Assumptions

1. 인터넷은 네트워크의 네트워크다
2. 게이트웨이는 연결 상태를 유지하지 않는다.
3. 라우팅 복잡성은 게이트웨이에 있어야한다
4. 시스템은 광범위한 네트워크의 변화를 수용할 수 있어야한다.

### 용어정리

**Multiplexing**

shared use of a single communications channel

**Internet Communication System**

`인터넷 통신 시스템`은 인터넷 프로토콜을 사용하는 호스트 컴퓨터 간의 통신을 지원하는 `상호 연결된 패킷 네트워크`로 구성된다.
