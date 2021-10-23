# IP

## IP Motivation

### 키워드

packet-switched, network, transmit, datagram, src dest, fragmentation, reaseembly

### 내용

- for use in interconnected systems of packet-switched computer communication networks
- provides for transmitting blocks of data called datagrams from sources to destinations.
- provides for fragmentation and reassembly of long datagrams

## IP Function : Addressing

### 키워드

routing

### 내용

- use the addresses carried in the internet header
- IP 는 names, address, routes 에서 차이가 발생하는데, names 를 통해 destination 을 알 수 있고, address 를 통해 현재 위치를 알 수 있으며, route 는 우리가 목적지에 어떻게 도달할지를 알려준다.

## IP Function : Fragmentation

### 키워드

independent entity, MTU

### 내용

- use fields in the IP header to fragment and reassemble internet datagrams when necessary for transmission through "small packet" networks
- treats each internet datagram as an independent entity
- MTU 는 네트워크 인터페이스에서 나뉘지 않고 전송될 수 있는 최대 데이터그램 크기다. IP Header 와 data 의 크기에 대한 제한 크기이다.

## Ipv4 Header

### 키워드

### 내용

![](https://i.imgur.com/HSINmoe.png)

- Version (4bits)
  IPv4 또는 IPv6 를 명시
- HLEN (4bits)
  4 byte 로 헤더의 길이를 나타냄 (4byte 라는 단위라는 것)
- Service Type
- Total Length
  헤더를 포함한 데이터그램의 총 길이를 나타냄

- Protocol
  다음 단계의 프로토콜을 명시
  이미 정해진 Assigned Numbers 가 있다.
  ex) TCP : 6, UDP : 17

- **Type of Service (TOS)** - IP 패킷 헤더 내에 있는 8비트 필드를 나타내며, 요구되는 서비스 질의 유형을 나타낸다. - IP 데이터 그램이 라우터에서 어떻게 처리되어야하는지를 정의한다.
  ex) actual transmission parameter, the network to be used for the next hop, the next gateway when routing an internet datagram

      - 2가지의 Traffic Classification Method 중 Behavior-Aggregate Classification 방법을 적용한 것이며, field 를 통해 해당 패킷의 중요도를 확인할 수 있다.

  ![](https://i.imgur.com/gyM6LSh.png)

- Time to live
  - 각각의 라우터는 해당 Packet 이 도달하면 TTL 을 1씩 감소시킴
  - 만약 패킷의 해당 값이 0 이 되면 패킷을 버린다. 잘못된 라우팅 테이블 매칭으로 인해 제 시간에 제 장소에 패킷이 전달되지 않을 수 있기 때문이다.

![](https://i.imgur.com/e6yc4AW.png)

- Identification

  - to ensure that fragments of different datagrams are not mixed

- Fragment offset

  - tells the receiver the position of a fragment in the original datagram <br/>
  - 64bits 단위로 측정된다. (8 byte)

- Flags

  - The more-fragments flag indicates (by being reset) the last fragment. These fields provide sufficient information to reassemble datagrams
  - D : Do not fragment (Fragment 를 안해도되는지)
  - M : More fragment (더 전송될 것이다, 1이면 더 전송될 것이라는 뜻)

- Header Checksum
  - The checksum is calculated at the sender and the receiver repeats the same calculation on the whole packet including the checksum.
