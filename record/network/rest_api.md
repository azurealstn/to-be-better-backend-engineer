# REST API

REST란, HTTP URI를 통해 자원을 표시하고 HTTP Method를 통해 자원에 대한 처리를 표현합니다.

REST API는 REST(REpresentational State Transfer) 아키텍처 스타일의 디자인 원칙을 준수하는 API이다. 이러한 이유로 REST API를 RESTful API라고도 한다.

## REST 구성요소

- 자원(Resource) : HTTP URI
- 자원에 대한 행위(Verb) : HTTP Method
- 자원에 대한 행위의 내용 (Representations) : HTTP Message Pay Load

## REST API 설계

문서: https://restfulapi.net/resource-naming/

1. URI는 동사보다는 명사를, 대문자보다는 소문자를 사용하여야 한다.

```java
Bad: /Order
Good: /order
```

2. 마지막에 슬래시 (/)를 포함하지 않는다.

```java
Bad: /Order/
Good: /order
```

3. 언더바나 카멜케이스 대신 하이폰을 사용한다.

```java
Bad: /userInfo, /user_info
Good: /user-info
```

4. 파일확장자는 URI에 포함하지 않는다.

```java
Bad: /image.png
Good: /image
```

5. 행위를 포함하지 않는다.

```java
Bad: /create-members
Good: /members
```

### 컨트롤 URI

5번에서 행위를 포함해야 하는 경우도 생긴다. 이러한 경우에는 동사로된 리소스 경로를 그냥 사용하면 된다.

```java
/orders/{orderId}/start-delivery
```

`start-delivery`처럼 동사를 직접 사용하는 것을 컨트롤 URI라고 한다.

## References

- [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC#)
- https://khj93.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-REST-API%EB%9E%80-REST-RESTful%EC%9D%B4%EB%9E%80
- https://www.ibm.com/kr-ko/topics/rest-apis
