# HTTP

웹에서 HTTP는 HyperText Transfer Protocol의 약자로, 클라이언트에서 서버까지 일련의 흐름을 결정하는 프로토콜이다. HTTP는 리소스를 식별하는 URI를 식별하여 어떤 리소스인지 구분할 수 있다.

HTTP 메시지에 모든 것을 전송한다.

- HTML, TEXT
- 이미지, 음성, 영상, 파일
- JSON, XML (API)

## 기반 프로토콜

- TCP: HTTP/1.1, HTTP/2
- UDP: HTTP/3
- 현재는 주로 HTTP/1.1 사용

## HTTP 특징

- 클라이언트 - 서버 구조
- 무상태(Stateless): HTTP는 상태를 계속 유지하지 않는 무상태 프로토콜이다.
  - 장점: 무한한 서버 확장 가능 (스케일 아웃)
  - 단점: 로그인 풀림
- 비연결성(Connectionless): 요청 - 응답이 한번 수행되면 그 후로 해당 연결을 유지하지 않는다. 따라서 새로운 요청이 보내질 때 마다 새로운 응답이 생성된다.
  - 서버 자원을 효율적으로 사용 가능

### 지속연결(Persistent Connections)

HTTP의 특징중 하나가 비연결성(Connectionless)이라 했다. 따라서 요청 - 응답이 한번 수행될 때마다 TCP 3, 4 handshake 과정을 거치기 때문에 시간이 오래 걸린다.

이를 해결하기 위해 지속연결이 나온다.  
js, html, css 각각 리소스를 연결하고 종료하는 것이 아니라 한번 연결하고 모든 리소스를 가져와서 그제서야 종료하는 것이다. 이러면 TCP 커넥션의 연결과 종료의 반복되는 오버헤드를 줄여주기 때문에 서버에 대한 부하가 줄어든다. 이는 웹 페이지에 대한 성능을 높여주는 것이다.

## References

- [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC#)
