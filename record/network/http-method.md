# HTTP 메서드

HTTP는 요청 메서드를 정의하여, 주어진 리소스에 수행하길 원하는 행동을 나타낸다. 요청 메서드를 "HTTP 동사"라고 부르기도 한다.

## 주요 메서드

- GET: GET을 사용하는 요청은 오직 데이터를 받기만 한다. (리소스 조회)
- POST: POST 메서드는 특정 리소스에 엔티티를 제출할 때 쓰인다. (요청 데이터 처리)
- PUT: PUT 메서드는 목적 리소스 모든 현재 표시를 요청 payload로 바꾼다. (리소스를 대체하고 리소스가 없으면 생성)
- PATCH: PATCH 메서드는 리소스의 부분만을 수정하는 데 쓰인다. (리소스 부분 변경)
- DELETE: DELETE 메서드는 특정 리소스를 삭제한다. (리소스 삭제)

## 기타 메서드

- HEAD: GET과 동일하지만 응답 본문을 포함하지 않고, 상태줄과 헤더만 반환
- OPTIONS: OPTIONS 메서드는 대상 리소스의 통신을 설정하는 데 쓰인다. (주로 CORS에서 사용)
- CONNECT: CONNECT 메서드는 대상 리소스로 식별되는 서버로의 터널을 맺는다.
- TRACE: TRACE 메서드는 목적 리소스의 경로를 따라 메시지 loop-back 테스트를 수행한다. (거의 사용 X)

## GET vs POST

- GET은 데이터를 요청할 때, POST는 데이터를 처리할 때 사용
- GET은 캐시가 가능하지만, POST는 캐시가 불가능하다.
- GET은 브라우저 히스토리에 남지만, POST는 브라우저 히스토리에 남지 않는다.
- GET은 북마크 될 수 있지만, POST는 북마크 될 수 없다.
- GET은 브라우저마다 데이터 길이가 제한되지만, POST는 데이터 길이가 제한되지 않는다.
- GET은 쿼리 파라미터에 정보가 다 노출되어 보안에 취약하지만, POST는 HTTP 메시지 body에 담아서 보내기 때문에 보안에 좋다.

## References

- [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC#)
- https://developer.mozilla.org/ko/docs/Web/HTTP/Methods
