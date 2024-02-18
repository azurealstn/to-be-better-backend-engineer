# 엔티티 매핑

## 객체와 테이블 매핑

### @Entity

- @Entity가 붙은 클래스는 JPA가 관리하며, 엔티티라 한다.
- JPA를 사용해서 테이블과 매핑할 클래스는 @Entity가 필수이다.

#### **주의**

@Entity 를 사용하면 주의할 점이 있다.

- **기본 생성자 필수**이다. 따라서 파라미터가 없는 public 또는 protected 생성자를 생성한다. 보통은 protected 생성자를 사용하여 다른 곳에서의 기본 생성자 생성을 최소한으로 제한시킨다. (default, private ❌)
- final 클래스, enum, interface, inner 클래스를 사용할 수 없다. ❌
- 저장할 필드에 final 키워드를 사용할 수 없다. ❌
- @Entity의 속성으로 name이 있는데 JPA에서 사용할 엔티티 이름을 지정한다. 가급적 기본값을 사용하도록 권장한다.

### @Table

- @Table은 엔티티와 매핑할 테이블 지정한다.
- name 속성을 이용해 매핑할 테이블의 이름을 지정할 수 있다. 이것은 자주 사용한다. 예를 들어, Order 클래스는 DB에 order라는 테이블명으로 지정되는데, DB SQL문에는 order by 라는 키워드가 있기 때문에 name 속성을 이용해 orders로 변경한다.

### @Column

- 필드에 적용할 수 있으며, name 속성을 이용해 필드와 매핑할 테이블의 컬럼 이름을 지정할 수 있다.

### @Enumerated

- 자바 enum 타입을 매핑할 때 사용한다.
- value 속성이 있는데 `EnumType.ORDINAL`은 절대 사용하면 안된다. enum 타입의 순서를 DB에 저장하기 때문에 순서가 바뀌면 망한다.
- 따라서 `EnumType.STRING`으로 사용해야 enum 이름을 저장할 수 있다.

### @Temporal

- 날짜 타입(java.util.Date, java.util.Calendar)을 매핑할 때 사용한다.
- 자바 8 이상의 LocalDate, LocalDateTime을 사용할 때는 생략이 가능하다. (최신 하이버네이트 지원)
- 요즘은 잘 사용하지 않는다.

### @Lob

- 데이터베이스 BLOB, CLOB 타입과 매핑
- @Lob에는 지정할 수 있는 속성이 없다.
- 매핑하는 필드 타입이 문자면 CLOB 매핑, 나머지는 BLOB 매핑
  - CLOB: String, char[], java.sql.CLOB
  - BLOB: byte[], java.sql. BLOB

### @Transient

- 필드와 매핑하지도 않고, 데이터베이스에 저장이나 조회 또한 되지 않는다.
- 주로 메모리상에서만 임시로 어떤 값을 보관하고 싶을 때 사용한다.

### @Id, @GeneratedValue

기본키 매핑과 기본키 생성 전략을 지정할 수 있다.

#### 기본 키 매핑 방법

- 직접 할당: @Id만 사용
- 자동 생성(@GeneratedValue)
  - IDENTITY: 데이터베이스에 위임, MYSQL
  - SEQUENCE: 데이터베이스 시퀀스 오브젝트 사용, ORACLE
  - TABLE: 키 생성용 테이블 사용, 모든 DB에서 사용
  - AUTO: 방언에 따라 자동 지정, 기본값

기본키 생성 전략은 주로 `IDENTITY`를 사용하여 MySQL의 경우 AUTO\_ INCREMENT가 실행된다.

IDENTITY 전략은 `em.persist()` 시점에 즉시 INSERT SQL 실행하고 DB에서 식별자를 조회할 수 있다.

### 권장하는 식별자 전략

- 기본 키 제약 조건: null 아님, 유일, 변하면 안된다.
- 미래까지 이 조건을 만족하는 자연키는 찾기 어렵다. 대리키(대체키)를 사용하자.
- 예를 들어 주민등록번호도 기본 키로 적절하기 않다. - 자연키
- 권장: Long형 + 대체키 + 키 생성전략 사용 - 대리키(대체키)
- Long: Integer를 사용할 수도 있지만 10억 건수가 넘어가서 다시 Long으로 바꾸려고 하면 그게 더 힘들다. 따라서 Long으로 선언하는 것이 좋다.

## 데이터베이스 스키마 자동 생성

- DDL을 애플리케이션 실행 시점에 자동으로 생성한다.
- 테이블 중심 -> 객체 중심
- 데이터베이스 방언을 활용해서 데이터베이스에 맞는 적절한 DDL 생성한다.
- 이렇게 생성된 DDL은 개발 장비에서만 사용해야 한다.
- 생성된 DDL은 운영서버에서는 사용하지 않거나, 적절히 다듬은 후 사용할 수 있다.

### 데이터베이스 스키마 자동 생성 - 주의

- **운영 장비에는 절대 create, create-drop, update 사용하면 안된다.**
- 개발 초기 단계는 create 또는 update
  - 로컬과 개발 서버
- 테스트 서버는 update 또는 validate
- 스테이징과 운영 서버는 validate 또는 none
  - 사실 none 이라는 옵션은 없지만 관례상 넣으면 실행 자체가 안된다.
  - 운영서버는 가급적 none을 사용하고, script를 작성해서 개발 서버나 테스트 서버에서 충분히 테스트 검증 후에 운영 서버에 해당 script를 사용하면 된다.
  - 개발서버에서 update 를 사용하여 나온 쿼리문을 활용하여 운영에 적용해도 되지만 이때도 테스트 검증을 충분히 한 후에 적용하는 것이 좋다.

## References

- [자바 ORM 표준 JPA 프로그래밍 - 기본편](https://www.inflearn.com/course/ORM-JPA-Basic/dashboard)
