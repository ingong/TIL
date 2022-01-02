### Rest API 에 대해서 설명해주세요

API 설계의 중심에 자원이 있고, HTTP 메서드를 통해 이 자원을 처리하도록 설계하는 API 입니다.

**특성**

Uniform Interface

- 특정 자원에 대해 POST, GET, PUT/PATCH, DELETE 의 균일한 인터페이스만 사용

Stateless

- 상태에 의존하지 않음

Cacheable

- Last-modified 태그, E-Tag 사용가능

Self-descriptiveness

- REST API 메시지만을 보고도 의도가 이해 가능해야 함

Client-Server Architecture

- REST 서버는 API만을 담당함. 인증, 컨텍스트(세션, 로그인) 등 기능은 클라이언트 담당.

Layered Architecture

- 보안, 로드 밸런싱, 암호화 등을 위해서 계층을 추가할 수 있음
- Proxy, Gateway와 같은 네트워크 중간매체 사용 가능

## Reference

[REST API 제대로 알고 사용하기 : TOAST Meetup](https://meetup.toast.com/posts/92)
