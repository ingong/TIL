### **HTTP 란 무엇인가요?**

HyperTextTransferProtocol 의 약자이며, 웹에 내재된 프로토콜입니다.

### **HTTP 의 특징은 무엇인가요?**

클라이언트 서버 구조입니다. 또한 무상태성과 비연결성입니다. 무상태성이므로 수평확장에 용이합니다. HTTP 1.1 과 2.0 은 TCP 기반이며, 3.0 은 UDP 기반입니다.

### **비연결성을 극복하기 위해 HTTP는 어떠한 발전을 했나요?**

### HTTP Request 와 Response 에 대해서 말씀해주세요.

**HTTP Request**

Start Line : HTTP Method, Request Target, HTTP Version (3)

Header: Host, User-Agent, Accept(데이터 타입), Authorization (4)

**HTTP Response**

Start Line : Status Code, Status Txt, HTTP Version (3)

Header: Date, Content-Type, Cache-Control (3)

Body: 요청에 대한 응답값

### **HTTP 에서 사용하는 메서드에 대해서 아는대로 말해주세요.**

get, post, put, patch, delete 가 있습니다.

### get 과 post 에는 어떤 차이가 있나요?

`get` 은 요청의 데이터가 header 부분에 담겨서 전송되며, 서버에서 자원을 조회할 때 사용하는 메서드입니다.

`post` 는 요청의 데이터가 body 부분에 담겨서 전송되며, 서버의 값이나 상태를 추가할 때 사용합니다.

### **put 과 patch 에는 어떤 차이가 있나요?**

put 은 리소스의 모든 것을 업데이트 합니다. patch 는 리소스의 일부를 업데이트 합니다.

### 상태 코드의 특징에 대해서 알려주세요.

1xx : 요청을 받았으며 프로세스를 계속 진행합니다.

2xx : 요청을 성공적으로 받았으며, 인식했고, 수용하였습니다.

3xx : 요청 완료를 위해 추가적인 작업이 필요합니다.

4xx : 클라이언트 오류입니다.

5xx : 서버 오류입니다.
