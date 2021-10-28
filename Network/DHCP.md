## DHCP

Dynamic Host Configuration Protocol

IP 주소를 자동으로 할당하는 프로토콜

네트워크 관리자가 `IP 주소 할당`을 `중앙에서 관리`하고, `자동화`할 수 있다.

Boostrap protocol(BOOTP) 의 확장판이다.

### Purpose

1. `DHCP 서버`에서 호스트로 `호스트별 구성 매개변수` `전달`
2. 호스트에 대한 `네트워크 주소 할당`

### Three mechanisms for IP address allocation

Automatic, **Dynamic**, Manual

⇒ DHCP 가 한정된 시간에 대해서 클라이언트에게 IP 주소를 할당

### Design Goals

1. `Mechanisms`
2. `클라이언트`에서 `수동 재구성이 필요하지 않다.`
3. 개별 클라이언트에 대해 `네트워크를 수동으로 구성할 필요가 없다.`
4. DHCP 는 각 서브넷에 서버가 필요하지 않다. 중앙에서 관리할 수 있기 때문.
5. DHCP 는 BOOTP 의 릴레이 에이전트 동작과 상호 작동해야한다.
6. client 는 구성 매개 변수 요청에 대해 여러 응답을 수신할 준비를 해야한다.

### DHCP Interaction

Discover, offer, request, acknowledge

왜 4단계로 진행되는가?

DHCP 서버가 여러대가 있을 수 있기 때문에

### DHCP 의 구성요소

1. DHCP Server

   IP 주소 풀을 보유하고 client 에게 IP 주소를 분배한다.

2. DHCP Client
3. DHCP/BOOTP relay agent

   Broadcast packet 은 router 를 넘어갈 수 없다.

   종종 DHCP 서버는 라우터 넘어서에 존재할 수도 있다.

   DHCP Relay agent 는 router 에 존재하며, request 가 들어오면 해당 패킷을 unicast 로 바꾸고 DHCP 서버에게 전달한다. 서버도 동일하게 이를 router 에게 unicast 로 전달하고, router 에서 이를 broadcast 로 바꾼다.

### DHCP message format

- op : message op code (1 = Request, 2 = reply)
- htype : hardware address type
- hlen : hardware address length
- hops : client sets to zero
- xid (Transaction ID) : a random number chosen by the client
- Secs : Filled in by client
- Flags : Broadcast flag
- ciaddr : client IP address
- yiaddr : your client IP address
- **siaddr : IP addresss of next server to use in boostrap**
- giaddr : relay agent IP address
- chaddr : client hardware address
- sname : optional serer host name
- **options : server identifier option**

### DHCP Protocol (1)

1. **DHCP Discover**

Client `broadcast to locate available servers`

BOOTP relay agents may pass the msg on to DHCP servers (giaddr)

만약 giaddr field 가 비어있다면 relay agent 는 이를 요청받은 interface 의 IP 로 채워야하며, 0 이 아니라면 변경시켜서는 안된다.

1. **DHCP Offer**

Server offer `configuration parameters`

### DHCP Protocol (2)

Host 와 Router 는 원래 illegal IP address 가 illegal 하다면 discard 하게 되어있음. 이를 `Martian address filtering`

BOOTP relay agent 를 지원하는 host 나 router 는 이러한 local delivery 를 수용한다.

각각의 Server 는 yiaddr field 에 이용가능한 네트워크 주소를 채워서 전송한다.

서버는 이를 저장할 필요는 없지만, 해당 IP 주소가 사용중인지 아닌지는 확인해야한다.

1. The `client’s current address` as recorded in the client’s current binding

2. The client’s `previous address` as recorded in the client’s (now expired or released) binding if that address is in the server’s pool of available addresses and not already allocated

3. The address requested in the `’Requested IP Address’ option`, if that address is valid and not already allocated
4. `A new address` allocated from the server’s pool of available addresses

### DHCP Protocol (3)

프로토콜 소프트웨어가 IP 주소로 구성될 때까지 `유니캐스트 IP 데이터그램을 수신할 수 없는 클라이언트`는 클라이언트가 보내는 DHCPDISCOVER 또는 DHCPREQUEST 메시지에서 `'플래그' 필드의 브로드캐스트 비트를 1로 설정`해야 합니다.

### DHCP Protocol (4)

The servers receive the DHCPREQUEST broadcast
from the client
선택받은 `서버`는 `영구 스토리지`에 `클라이언트를 바인딩`하도록 커밋하고, 요청 클라이언트의 `구성 매개 변수를 포함하는 DHCPACK 메세지`로 응답한다.

### DHCP Protocol (5)

The client receives the DHCPACK message with
configuration parameters

클라이언트가 구성된다

## DHCP Operation

1. Client broadcast DHCPDISCOVER
2. Server respond with DHCPOFFER
3. Server check for address
4. Client broadcasts DHCPREQUEST
5. Server selected commits binding, send DHCPACK

## DHCP Advantage & Disadvantage

### Advantage ⇒ SFCD

Centralized administration of IP configuration

Dynamic host configuration

Seamless IP host configuration

Flexibility and scalability

### Disadvantage

DHCP Server is unavailable, 접근 불가

Uses UDP, unreliable insecure

Security Problem - Spoofing

## Message

**DISCOVER**

Source Mac Address : 각자꺼

Source IP Address 0.0.0.0

DEST IP Address 255.255.255.255

Client Hardware Address = PC MAC address

DHCP Message Type = 1

**OFFER**

Source Mac Address : 각자꺼

`Source IP Address 1.1.1.254`

DEST IP Address 255.255.255.255

Your IP Address 1.1.1.10

Client Hardware Address = PC MAC address

Subnet Mask = 255.255.255.0(/24)

Router IP = 1.1.1.1 (Default Gateway)

Domain Name Server IP = 10.1.1.1, 10.1.1.2

`DHCP Server Identifier 1.1.1.254`

DHCP Message Type = 2

IP Address Lease Time

**REQUEST**

Source Mac Address : 각자꺼

DHCP Message Type = 3

Your IP Address : 0.0.0.0
Requested IP Address : 1.1.1.10

OFFER 에서 받은 yiaddr

**Ack**

Source Mac Address : 각자꺼

DHCP Message Type = 5

Subnet Mask = 255.255.255.0(/24)

Router IP = 1.1.1.1 (Default Gateway)

Domain Name Server IP = 10.1.1.1, 10.1.1.2

IP Address Lease Time

## BOOTP

BOOTP 는 호스트 정보를 수동으로 사전 구성하도록 설계되었다.
