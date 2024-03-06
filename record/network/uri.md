# URI, URL, URN

![uri](/record/network/images/uri-1.png)
(출처: https://hstory0208.tistory.com/entry/URI%EC%99%80-URL-%EB%B9%84%EC%8A%B7%ED%95%B4%EB%B3%B4%EC%9D%B4%EB%8A%94%EB%8D%B0-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%B4-%EB%AD%98%EA%B9%8C-%EC%99%84%EB%B2%BD-%EC%A0%95%EB%A6%AC)

## URI

URI는 Uniform Resource Identifiers의 약자로, 스키마를 나타내는 리소스를 식별하기 위한 식별자이다. 스키마는 리소스를 얻기 위한 수단에 이름을 붙이는 방법이다.

> `https://www.google.co.kr`에서 `https`가 스키마다.

통합 자원 식별자(Uniform Resource Identifier, URI)는 인터넷에 있는 자원을 나타내는 유일한 주소이다.

URI는 로케이터(Locator), 이름(Name) 또는 둘 다 추가로 분류될 수 있다.

> URI에는 URL과 URN을 포함한다.

## URL

URL은 Uniform Resource Locator의 약자로, 웹에서 주어진 고유 리소스 주소이다.

URL로 표시되는 리소스와 URL 자체는 웹 서버에서 처리되므로 해당 리소스와 관련 URL을 신중하게 관리하는 것은 웹 서버 소유자에게 달려 있다.

- scheme://[userinfo@]host[:port][/path][?query][#fragment]
- https://www.google.com:443/search?q=hello

- scheme: 주로 프로토콜 사용
- userinfo: URL에 사용자정보를 포함해서 인증 (거의 사용 X)
- host: 호스트명 (도메인명, IP 주소)
- PORT: 접속 포트 (생략시 http는 80, https는 443)
- path: 리소스 경로, 계층적 구조(/home/file1.jpg)
- query: key=value 형태 (query parameter, query string으로 불림)
- fragment: html 내부 북마크 등에 사용 (서버에 전송하는 정보 X)

## URN

URN(Uniform Resource Name, 통합 자원 이름)은 urn:scheme 을 사용하는 URI를 위한 이름이다. URN은 영속적이고, 위치에 독립적인 자원을 위한 지시자로 사용한다.

> URN은 거의 사용하지 않는다.

## References

- [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC#)
