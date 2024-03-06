# HTTP 메시지

HTTP에서 교환하는 정보를 HTTP 메시지라 불리는데 요청할 때 HTTP 메시지를 요청 메시지, 응답할 때 HTTP 메시지를 응답 메시지라 부른다.

TCP/IP 통신할 때 패킷에는 HTTP 메시지가 포함되어 있다.

![http-message-1](/record/network/images/http-message-1.png)

## HTTP 요청 메시지

### start-line

HTTP 요청은 서버가 특정 동작을 취하게끔 만들기 위해 클라이언트에서 전송하는 메시지이다.

- HTTP 메서드: POST
- URL: /
- HTTP 버전: HTTP/1.1

### header

![http-message-2](/record/network/images/http-message-2.png)

요청에 들어가는 HTTP 헤더는 HTTP 헤더의 기본 구조를 따른다.

- HTTP 전송에 필요한 모든 부가정보 포함

### HTTP 메시지 바디 (본문)

본문은 요청의 마지막 부분에 들어간다.  
모든 요청에 본문이 들어가지는 않는다. GET, HEAD, DELETE, OPTIONS처럼 리소스를 가져오는 요청은 보통 본문이 필요가 없다.

## HTTP 응답 메시지

![http-message-3](/record/network/images/http-message-3.png)

### start-line

클라이언트의 요청을 처리하여 서버에서 전송하는 메시지이다.

- HTTP 버전: HTTP/1.1
- 상태코드: 200
- 상태코드 메시지: OK

### header

- 응답에 들어가는 HTTP 헤더는 다른 헤더와 동일한 구조를 따른다.
- 대소문자를 구분하지 않는다.

### HTTP 메시지 바디 (본문)

- 실제 전송할 데이터
- HTML 문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터들이 전송 가능하다.

## References

- https://developer.mozilla.org/ko/docs/Web/HTTP/Messages
- [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC#)
