# HTTP 헤더

HTTP 헤더의 용도는 HTTP 전송에 필요한 모든 부가정보들을 전송할 수 있도록 해준다.

## HTTP Body

- 메시지 본문(message body)을 통해 표현 데이터 전달
- 메시지 본문 = 페이로드(payload)
- **표현**은 요청이나 응답에서 전달할 실제 데이터
- **표현 헤더**는 **표현 데이터**를 해석할 수 있는 정보
  - 데이터 유형(html, json), 데이터 길이, 압축 정보 등등

> Representation = Representation Metadata + Representation Data  
> 표현 = 표현 메타데이터 + 표현 데이터  
> RESTful의 R이 Representation이다.

## 표현 헤더

- **Contnet-Type:** 표현 데이터의 형식 - Message Body의 내용이 어떤 타입인지.
  - 미디어 타입, 문자 인코딩
  - text/html; charset=utf-8
  - application/json
  - image/png
- **Content-Encoding:** 표현 데이터를 압축하기 위해 사용
  - 어떤걸로 압축했는지.
  - gzip
  - deflate
  - identity
- **Content-Language:** 표현 데이터의 자연언어
  - ko
  - en
  - en-US
- **Content-Length:** 표현 데이터의 길이
  - 바이트 단위
  - Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안된다.

## 콘텐츠 협상

콘텐츠 협상이란 동일한 URI에서 리소스의 서로 다른 버전을 제공하기 위해 사용하는 메커니즘으로, 클라이언트가 선호하는 표현을 요청한다. 즉, 사용자 에이전트가 사용자에게 제일 잘 맞는 것이 무엇인지를 명시할 수 있다.

> 협상 헤더는 요청시에만 사용한다.

- **Accept**: 클라이언트가 선호하는 미디어 타입 전달
  - Accept: text/\*, text/plain, text/plain;format=flowed, "/"
  - 구체적인 것이 우선순위가 높다.
- **Accept-Charset**: 클라이언트가 선호하는 문자 인코딩
- **Accept-Encoding**: 클라이언트가 선호하는 압축 인코딩
- **Accept-Language**: 클라이언트가 선호하는 자연언어
  - 언어 우선순위
  - Quality Values(q) 값 사용
  - 0~1, 클수록 높은 우선순위
  - Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7

## 일반정보

- **From**: 유저 에이전트의 이메일 정보
  - 검색 엔진에서 주로 사용
- **Referer**: 현재 요청된 페이지의 이전 웹 페이지 주소
  - Referer를 통해 유입 경로 분석 가능
- **User-Agent**: 유저 에이전트 애플리케이션 정보
  - 클라이언트의 애플리케이션 정보 (웹 브라우저 정보 등등)
  - 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
  - 통계 정보
- **Server**: 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
  - Server: Apache/2.2.22 (Debian)
  - Server: nginx
  - 응답에서 사용
- **Date**: 메시지가 발생한 날짜와 시간
  - 응답에서 사용

## 특별한 정보

- **Host**: 요청한 호스트 정보 (도메인) - 필수
  - 하나의 서버가 여러 도메인을 처리해야 할 때 사용
- **Location**: 페이지 리다이렉션
  - 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 이동한다. (리다이렉션)
- **Allow**: 허용 가능한 HTTP 메서드
  - 405 (Method Not Allowed)에서 응답 포함해야 한다.
- **Retry-After**: 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
  - 503 (Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있다.

## 인증

- **Authorization**: 클라이언트 인증 정보를 서버에 전달
  - Authorization: Basic xxxxxxxxxx
- **WWW-Authenticate**: 리소스 접근시 필요한 인증 방법 정의
  - 401 Unauthorized 응답과 함께 사용한다.

## References

- [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC#)
