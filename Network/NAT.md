NAT(Network Address Translator)

Private 주소를 global ip 주소에 대한 매핑. 머신이다.

한 가정, 회사에서만 식별이 가능한 주소

`이러한 장점이 있고, 추가적인 Operation 이 필요하다`

Basic NAT : private IP 와 public IP 가 1 : 1, Src Ip 는 밖에서는 유효하지 않아. 그 전에 어드레스 바인딩. NAT Inside IP 10.1.1.1 NAT Outside IP 5.5.5.1 로 바꾼다. 들어올 때도 Dst IP 를 NAT Inside 로 바꾼다. 주소가 부족해서 NAT 를 쓴다. Address 할당 효율은 맞지 않다. Inside 와 Outside 를 다르게 해서 Security 를 챙겼다. Outbound: private → public / Inbound : public → private, IP Header Checksum 은 IP Header 가 하나라도 바뀌면 바뀌어야했기 때문이다.

NAPT(Network Address Port Trasnlation) priavet IP 와 public IP → N : 1, 이를 식별하기 위해 Port 가 있다. 1 : N Mapping. NAPT Outbound port 도 바꾼다!! Inbound (public → private) Source IP Address, Header Checksum, TU Source Port, TCP/UDP Checksum (Port 를 바꾸기 때문에) , Checksum 계산 2번하기 때문에, Computation Overhead 야기시킬 수 있다.
