### Transport Layer

End Point 간 **`신뢰성`**있는 `**데이터 전송**`을 담당하는 계층

신뢰성 : 데이터를 순차적, 안정적인 전달

전송: **포트 번호**에 해당하는 프로세스에 데이터를 전달

### TCP

TCP 는 신뢰성있는 데이터 통신을 가능하게 해주는 프로토콜입니다. 3-way handshake 를 통해 연결하며, 데이터의 순차 전송을 보장합니다.

### TCP 의 특징에 대해서 설명해주세요

Flow Control, Congestion Control, Error Detection 을 담당합니다. 데이터의 단위를 Segment 라고 합니다. Application 에서 받은 Data 를 자르고, TCP Header 와 Data 를 합쳐서 Segment 라고 한다. TCP Header 의 flags field 를 통해 TCP 연결을 제어하고, 데이터를 관리합니다.

### TCP 의 3-way handshake

Segment Header 의 flag field 를 설정해 연결하는 방식입니다. ACK, SYN, FIN 패킷을 사용하며, 연결을 성립하는데 양방향 모두 ACK 패킷이 필요하기 때문에 3-way 가 필요합니다.

`SYN` → Synchronize sequence number, `ACK` → Acknowledgement

**연결 성립**

먼저 Clinet 에서 Server 로 SYN 을 보냅니다. Server 에서는 SYN 값을 기반으로 ACK 로 설정하고, ACK 와 SYN 을 보냅니다. 마지막으로 Client 에서 Server 로 받은 SYN 값을 기반으로 ACK 값을 설정하고 서버에 전송합니다.

**연결 해제**

1. 데이터를 전부 송신한 Client 가 FIN 송신
2. Server 가 ACK 송신
3. 일정 시간을 대기하고, Server 에서 남은 패킷 송신 (아직 남은 데이터가 있을 수 있기 때문)
4. Server 가 FIN 송신
5. Client 가 ACK 송신 (서버도 상태를 Close 한다)

### TCP 의 문제점

- 전송의 신뢰성은 보장하지만 매번 연결해서 시간 손실 발생
- 패킷을 조금만 손실해도 재전송

### UDP

TCP 보다 신뢰성이 떨어지지만 전송 속도가 일반적으로 더 빠른 프로토콜입니다. Connectionless 하며 체크섬에서 Error Detection 기능만 작동하며, 데이터의 신뢰성이 중요하지 않을 때 사용합니다.

TCP 와 다르게 데이터를 쪼개지 않고, UDP Header 를 더해준다.

## 준수님 답변

### **연결 성립(3-way)**

1. Client → Server : SYN(a)
2. Server → Client: ACK(a + 1), SYN(b)
3. Client → Server: ACK(b + 1)

- 양방향 ACK이 필요하기 때문에, 2-way로는 부족하고 3-way가 필요하다.
  - 양쪽에서 서로 메시지 전송이 됨을 확인.
- SYN 패킷에 난수가 있는 경우
  - 포트 재사용으로 인한 이전 요청(순차적 Sequence 수)와 구분하기 위해서

### 연결 해제(4-way)

1. Client → Server: FIN
2. Server → Client: ACK
   1. 보내던 것 계속 보냄 → TIME_OUT 상태
   2. 전송이 모두 끝내면 FIN
3. Client → Server: ACK
4. Server : Socket 연결 종료
5. Client : 이전에 보낸 데이터를 잠시 기다림 → TIME_WAIT 상태
