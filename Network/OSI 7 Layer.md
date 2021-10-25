## Application Layer

네트워크를 통해 데이터를 보내고 받을 수 있는 `플랫폼을 제공`한다.

ex) Browser, Email Client

## Presentation Layer

클라이언트의 요청을 전달하기 위해 서버가 이해할 수 있는 데이터로 `변환`하거나, 서버의 데이터를 클라이언트가 이해할 수 있게 변환한다.

ex) Data Encrpytion and decryption, Character Encoding, Data Compression

## Session Layer

양 끝단의 `응용 프로세스와 응답 간의 세션`을 관리하기 위한 매커니즘

TCP/IP 세션을 만들고 없애는 책임을 가진다.

1. Dialog control : 두 개의 응용 프로세스가 대화에 참여할 수 있게 하며, 누가 전송할 차례인지를 유지한다.
2. Synchronization : add check point into stream of data
3. Multiplexing
4. Error Connection

   전송에 동기화 포인트를 삽입하여 메시지를 대화에 그룹화하며, 만약 에러가 발생한 경우에는 해당 부분부터 재전송한다.

5. 세션을 생성하고 닫는 역할을 한다. 논리적 연결관계를 만드는 것을 의미한다. 토큰을 사용한다.

## Transport Layer

목적지에 `신뢰할 수 있는 데이터 전달`하기 위해서 필요하다.

1. `오류를 점검`하는 기능을 가지고 있다.
2. 전송된 `데이터의 목적지`가 어떤 어플리케이션인지 `식별`한다.

### TCP (연결형 통신 프로토콜)

신뢰할 수 있고 정확하게 데이터를 전송하는 통신 방식

- 연결형 통신을 하기 위해서는 데이터를 전송하기 전에 가상의 독점 통신로를 확보해야한다.
- 연결을 확힙하기 위해 TCP 헤더에 있는 코드 비트를 사용한다

코드 비트 중 SYN 은 연결 요청, ACK 는 연결 응답, FIN 은 연결 종료

SYN 으로 X 를 보내면, ACK 로 X + 1 을 보낸다.

- **세그먼트(segment)**

TCP 헤더가 붙은 데이터

- **3-way 핸드셰이크**

연결 확립을 위해 패킷 교환을 3번 하는데, 이를 나타내는 용어이다.

### UDP (비연결형 통신 프로토콜)

효율성을 중요하게 여기는 프로토콜, 데이터를 효율적이고 빠르게 보낼 수 있다.

- UDP 데이터 그램

UDP 헤더가 붙은 데이터

### Transport Layer 의 주요한 5가지 기능 `(CCSRF)`

1. Connection Management

   TCP's 3-way handshaking

2. Connection Multiplexing

   Allow multiple applications to simultaneously send and recieve data

   `소켓`은 두 프로그램이 네트워크를 통해 서로 통신을 수행할 수 있도록 양쪽에 생성되는 링크의 단자다. 소켓이 연결되면 서로 다른 프로세스간 데이터 전달이 가능하다. 소켓을 통해 네트워크 및 전송 계층의 캡슐화가 가능.

3. Segmentation

   데이터를 더 작은 단위로 나누는 것이다. TCP data field 에 들어가기 위해서 적절한 크기로 쪼개서 담긴다.

   MTU(Maximum Transfer Unit) : 한 패킷으로 전송할 수 있는 최대 단위의 크기.

   MSS(Maximum Segment Unit) : 한 패킷에 각종 Header 를 제외한 순수 데이터 크기이다.

4. Reliable and unreliable data delivery
5. `Flow Control and Congestion Control`

   - Flow Control

   송신측과 수신측의 `데이터처리 속도 차이`를 해결하기 위한 기법

   수신측에서 제한된 저장용량(일반적으로 큐)을 초과하여 이후에 도착하는 데이터의 손실을 가져올 수있다.

   강제로 송신측의 데이터 전송을 줄인다.

- Congestion Control

송신측의 `데이터 전달`과 `네트워크의 처리속도 차이`를 해결하기 위한 기법

라우터가 혼잡할 경우 라우터는 자신에게 온 데이터를 모두 처리할 수 없다. 그렇게 되면 호스트들은 또 다시 재전송을 하게 되고 결국 혼잡을 가중시켜 오버플로우나 데이터 손실을 발생한다.

송신측에서 보내는 데이터의 전송 속도를 강제로 줄이게 된다

두 방법 모두 송신측의 데이터 전송 속도를 강제로 줄인다는 점은 동일하다. 하지만 Flow Control 은 송신측의 데이터 처리 속도가 수신측의 데이터 처리속도보다 빨라서 발생하는 문제이며, Congestion Control 은 송신측의 데이터 전달과 `네트워크의 처리속도의 차이`를 해결하기 위한 기법이다.

## Netowrk Layer - IP

`라우팅을 통해 패킷을 소스로부터 Destination 까지 보낸다.`

- Internetworking : 네트워크 간의 통신을 가능하게 한다
- Logical Addressing: 네트워크를 식별할 수 있는 주소(IP 주소) 지정 체계를 정의
- LAN 안에서는 MAC 주소만으로도 통신이 가능하지만 네트워크 간에 통신을 하려면 IP 주소가 필요하다.
- 라우터 : 해당 목적지까지 어떤 경로로 가는 것이 좋은지 알려주는 기능
- 모든 인터넷 전송 프로토콜은 IP 를 사용하여 소스 호스트에서 대상 호스트로 데이터를 전송.
- IP 는 `종단간 전달 보장`이 없는 무접속 또는 데이터그램 인터넷 종단 간 서비스이다 ⇒ Best effort Delivery

## Datalink Layer

- `네트워크 장비 간에 신호를 주고받는 규칙을 정하는 계층`. 가장 자주 사용되는 규칙이 이더넷이다.
- 패킷의 대상에 대한 물리적, 논리적 연결을 처리한다
- Convert them into frames, adding physical address of the network card of your computer, and a checksum data
- error-free transfer 를 제공한다.
- Why does this flow control work in the transport
  layer and in the datalink layer?
  Because there are differences in the scope of flow
  control

## Physical Layer

`컴퓨터와 네트워크 장비를 연결`하고, 컴퓨터와 네트워크 장비 간에 전송되는 `데이터를 전기 신호로 변환`하는 계층이다.

## Advantages of OSI 7 Layer

- `prevents` changes in one layer from `affecting other layers`
- what functions occur at each layer of the model that encourages industry `standardization`
- makes software development, design and troubleshooting `easier`
- allows `different types of network hardware and software to communicate`
- multiple-vendor development
- make `network administartors` life eaiser
- makes learning easier
