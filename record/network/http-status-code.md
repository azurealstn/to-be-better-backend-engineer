# HTTP 상태코드

클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능이다.

- 1xx: 요청이 수신되어 처리중 (거의 사용하지 않음)
- 2xx: 요청 정상 처리
- 3xx: 요청을 완료하려면 추가 행동이 필요
- 4xx: 클라이언트 오류
- 5xx: 서버 오류

## 2xx - 성공

클라이언트의 요청을 성공적으로 처리

- **200 OK**: 요청 성공
- **201 Created**: 요청 성공해서 새로운 리소스가 생성됨
  - POST는 서버에서 신규 리소스를 생성한다. (컬렉션)
- **202 Accepted**: 요청이 접수는 되었으나 처리가 완료되지 않음
  - 배치 처리 같은 곳에서 사용
  - 잘 사용하지 않는다.
- **204 No Content**: 서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음
  - save 버튼의 결과로 아무 내용이 없어도 되는 경우

## 3xx - 리다이렉션

요청을 완료하기 위해 유저 에이전트의 추가 조치 필요

> 리다이렉트: 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동으로 이동한다.

### 영구 리다이렉션

특정 리소스의 URI가 영구적으로 이동

- **301 Moved Permanently**: 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(MAY)
- **308 Permanent Redirect**: 리다이렉트시 요청 메서드와 본문 유지 (처음 POST를 보내면 리다이렉트도 POST, 본문도 그대로 유지)

### 일시 리다이렉션

리소스의 URI가 일시적으로 변경

- **302 Found**: 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(MAY)
- **307 Temporary Redirect**: 리다이렉트시 요청 메서드와 본문 유지 (처음 POST를 보내면 리다이렉트도 POST, 본문도 그대로 유지)
- **303 See Other**: 리다이렉트시 요청 메서드가 GET으로 변경

### 기타 리다이렉션

- **304 Not Modified**: 캐시를 목적으로 사용
  - 클라이언트에게 리소스가 수정되지 않았음을 알려준다. 따라서 클라이언트는 로컬 PC에 저장된 캐시를 재사용한다. (캐시로 리다이렉트)
  - 304 응답은 메시지 바디를 포함하면 안된다. (로컬 캐시를 사용해야 하므로)
  - 조건부 GET, HEAD 요청시 사용

## 4xx - 클라이언트 오류

오류의 원인이 클라이언트에 있으며, 중요한 점은 클라이언트가 잘못된 요청을 했기 때문에 계속 재시도 해도 실패하게 된다.

- **400 Bad Request**: 클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음
- **401 Unauthorized**: 클라이언트가 해당 리소스에 대한 인증이 필요함
  - 401 오류 발생시 응답에 WWW-Authenticate 헤더와 함께 인증 방법을 설명
- **403 Forbidden**: 서버가 요청을 이해했지만 승인을 거부함
  - 주로 인증 자격 증명은 있지만, 접근 권한이 불충분한 경우
- **404 Not Found**: 요청 리소스를 찾을 수 없음

## 5xx - 서버 오류

4xx 오류와 반대로 서버에 문제가 있기 때문에 계속 재시도 하면 성공할 수 있다.

- 503 Service Unavailable: 서비스 이용 불가
  - 서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없음

## References

- [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC#)
