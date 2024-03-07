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

## PUT vs PATCH

### PUT

PUT은 리소스가 있으면 대체, 없으면 새로 생성한다.

```java
PUT /members/100 HTTP/1.1
Content-Type: application/json
{
  "username": "kim",
  "age": 30
}
```

위와 같이 PUT으로 회원정보를 생성했다. 그리고 아래와 같이 `age=50`으로 수정했다.

```java
PUT /members/100 HTTP/1.1
Content-Type: application/json
{
  "age": 50
}
```

PUT은 리소스를 완전히 대체하기 때문에 일부 데이터만 보내면 `username` 데이터는 사라진다. (대형 사고!) 따라서 이 경우엔 **PATCH 메서드**를 사용해야 한다.

> PUT의 메커니즘은 수정이 아닌 완전히 대체하는 것이다.

### PATCH

```java
PUT /members/100 HTTP/1.1
Content-Type: application/json
{
  "age": 50
}
```

부분 수정만 하려면 위와 같이 `age` 데이터만 보내도 `username`은 사라지지 않는다.

> PATCH는 부분 수정을 하는 경우 사용한다.  
> PATCH를 지원하지 않는 서버가 있는데 이 떄는 POST를 사용하면 된다.

## 속성

### 안전(Safe)

(리소스가 변경되지 않는 것 한해서) 리소스를 여러번 호출해도 변경되지 않는다. 즉, 동일한 리소스를 여러번 호출한 경우에 변경되지 않는다.

- GET, HEAD, OPTIONS, TRACE -> Safe
- POST, PUT, PATCH, DELETE, CONNECT -> Not Safe

### 멱등(Idempotent)

한번 호출하든 두번 호출하든 100번 호출하든 결과가 같아야 한다.

- GET, PUT, DELETE -> 멱등하다.
- POST -> 멱등하지 않다.

#### 멱등 활용

- 자동 복구 메커니즘: 서버가 timeout 등으로 정상 응답을 못주었을 때, 클라이언트가 같은 요청을 다시 해도 되는가 - 판단 근거가 된다.

## References

- [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC#)
- https://developer.mozilla.org/ko/docs/Web/HTTP/Methods
