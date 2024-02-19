# OSIV

OSIV는 약자로, 하이버네이트(Hibernate)에서는 Open Session In View, JPA에서는 Open EntityManager In View로 사용되는데 관례상 OSIV라 한다.

OSIV는 영속성 컨텍스트의 생존 범위를 결정하는 옵션 기능이다. JPA를 사용하면 OSIV를 끄고 킬 수 있다. 스프링 부트를 사용하면 `application.properties` 파일에서 `spring.jpa.open-in-view`로 옵션을 설정할 수 있다. 기본값은 true이다.

## OSIV ON

![osiv-1](https://github.com/azurealstn/to-be-better-backend-engineer/assets/55525868/5a8e80d4-a1dd-4787-b414-5083952cb8bc)

### `spring.jpa.open-in-view=true`

true로 설정하면 OSIV ON 상태가 된다. ON 상태는 트랜잭션 시작(@Transactional)시 DB 컨넥션을 연결하고 API의 경우 완전히 데이터 응답시 View의 경우 사용자에게 완전히 렌더링될 때까지 DB 컨넥션을 연결하고 있다가 종료된다.

OSIV를 활성화시키면 트랜잭션 시작처럼 최초 데이터베이스 커넥션 시작 시점부터 API 응답이 끝날 때 까지 영속성 컨텍스트와 데이터베이스 커넥션을 유지한다. 그래서 View Template이나 API 컨트롤러에서 지연 로딩이 가능하다.

지연 로딩은 영속성 컨텍스트가 살아있어야 가능하고, 영속성 컨텍스트는 기본적으로 데이터베이스 커넥션을 유지한다. 이것만으로도 엄청난 장점이 된다.

하지만 뭐든지 트레이드 오프가 있다. 해당 전략은 너무 오랜시간동안 데이터베이스 커넥션 리소스를 사용하기 때문에, 실시간 트래픽이 중요한 애플리케이션에서는 커넥션이 모자랄 수 있다. 이것은 결국 장애로 이어진다. 예를 들어서 컨트롤러에서 외부 API를 호출하면 외부 API 대기 시간 만큼 커넥션 리소스를 반환하지 못하고, 유지해야 한다.

## OSIV OFF

![osiv-2](https://github.com/azurealstn/to-be-better-backend-engineer/assets/55525868/6aac283d-0b2b-4ac6-b314-c84d1c4539fb)

### `spring.jpa.open-in-view=false`

false로 설정하면 OSIV OFF 상태가 된다. OFF 상태는 트랜잭션 시작(@Transactional)시 DB 컨넥션을 연결하고 트랜잭션이 종료될 때 DB 컨넥션도 같이 반환된다.

따라서 OSIV를 끄면 트랜잭션을 종료할 때 영속성 컨텍스트를 닫고, 데이터베이스 커넥션도 반환하여 커넥션 리소스를 낭비하지 않는다.

다만 OSIV를 끄면 모든 지연로딩을 트랜잭션 안에서 처리해야 하기 때문에 지연 로딩 코드를 트랜잭션 안에서 끝내야 하는 단점이 있다.

### 언제 사용?

고객 서비스의 실시간 API는 OSIV를 끄고, ADMIN 처럼 컨넥션을 많이 사용하지 않는 곳에서는 OSIV를 키면 좋을 것 같다.
