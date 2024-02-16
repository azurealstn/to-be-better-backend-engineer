# 영속성 컨텍스트

JPA에서 가장 중요한 2가지가 있다.

- 객체와 관계형 데이터베이스 매핑하기 (Object Relational Mapping)
- 영속성 컨텍스트

## 영속성 컨텍스트

- JPA를 이해하는데 가장 중요한 용어
- “엔티티를 영구 저장하는 환경”이라는 뜻
- `EntityManager.persist(entity);`
- 영속성 컨텍스트는 논리적인 개념이고, 엔티티 매니저를 통해 영속성 컨텍스트에 접근한다.

### 엔티티의 생명주기

#### 비영속 (new/transient)

- 영속성 컨텍스트와 전혀 관계가 없는 새로운 상태이다.
- `Student student = new Student();` 처럼 객체를 생성한 상태를 비영속 상태라고 한다.

#### 영속 (managed)

- 영속성 컨텍스트에 관리되는 상태
- `em.persist(student)`를 사용하면 객체가 저장되고, 영속 상태가 된다. 이 때부터 영속성 컨텍스트가 관리하게 된다.

#### 준영속 (detached)

- 영속성 컨텍스트에 저장되었다가 분리된 상태
- `em.detach(student);`를 사용하면 영속성 컨텍스트에서 분리시켜 준영속 상태가 된다.

#### 삭제 (removed)

- 삭제된 상태
- `em.remove(student);`를 사용하면 객체를 완전히 삭제한다.

### 영속성 컨텍스트의 장점 5가지

#### 1. 1차 캐시

![first-cache](https://github.com/azurealstn/to-be-better-backend-engineer/assets/55525868/93693ef2-fa6e-4e4b-9fdd-d8d03a200ae9)

위에서 설명한 엔티티의 생명주기에서 `student` 객체를 비영속 상태에서 영속화하면 즉, `em.persist(student)`를 사용하면 영속성 컨텍스트 내부에 1차 캐시라는 저장소에 `student` 객체를 저장하게 된다.

1차 캐시에 저장하면 좋은 점이 앞으로 `student` 객체를 조회할 때 DB를 통해 조회하는 것이 아니라 1차 캐시 메모리를 통해 조회한다. 그러면 DB 컨넥션을 통한 네트워크 시간을 줄일 수 있고, 빠르게 조회할 수 있다.

> `student` 객체가 1차 캐시에 없으면 DB를 통해 조회한다. 그리고 DB에서 조회한 결과를 다시 1차 캐시에 저장해서 데이터를 1차 캐시를 통해 가져온다.

<br>

#### 2. 동일성(identity) 보장

```java
Student a = em.find(Student.class, "student");
Student b = em.find(Student.class, "student");

System.out.println(a == b); // 동일성 비교 true
```

같은 트랜잭션 안에서 `em.find()`를 사용하여 같은 동일한 객체를 가져와도 서로 동일성을 보장한다.

<br>

#### 트랜잭션을 지원하는 쓰기 지연 (transactional write-behind)

![write-lazy](https://github.com/azurealstn/to-be-better-backend-engineer/assets/55525868/d392f28a-c234-481a-9653-1413931609f0)

1. `em.persist(studentA);`를 사용하면 `studentA` 객체가 1차 캐시에 저장된다.
2. `em.persist(studentB);`를 사용하면 `studentB` 객체가 1차 캐시에 저장된다.
3. 1번과 2번 각각 1차 캐시에 저장할 때 쓰기 지연 SQL 저장소에서 SQL문(INSERT)을 저장한다. 즉, 실제로 DB INSERT 쿼리문을 날리지 않고, 일단 쓰기 지연 SQL 저장소로 SQL문들을 저장하는 것이다.
4. 마지막으로 트랜잭션 커밋할 때 쓰기 지연 SQL 저장소에 있는 SQL문들을 모두 DB에 `flush`한다. DB에서는 플러시된 SQL문들을 실행해서 커밋한다.

> 플러시(flush)란 영속성 컨텍스트의 변경 내용을 DB에 반영하는 것을 말한다. 플러시가 발생한다고 DB에 실제 반영되는 것이 아니다. 실제 commit을 날려야 DB에 반영된다.  
> 즉, 플러시는 영속성 컨텍스트의 변경 내용을 DB에 동기화 시켜준다.

<br>

#### 변경 감지(Dirty Checking)

1차 캐시에는 스냅샷이라는 것이 있다. 변경감지는 트랜잭션 커밋할 때 영속화된 Entity에서 가지고 있었던 최초 정보(스냅샷)와 바뀐 Entity 정보를 비교해서 바뀐 부분이 있다면 Update SQL문을 생성하여 `flush`한다. 그리고 DB에서 플러시된 SQL문을 실행하여 커밋한다.

따라서 변경하려는 Entity가 기본적으로 영속 상태여야 한다. 만약 `studentA` 객체가 영속 상태이면 `setName("MIKE")`을 통해 이름을 MIKE로 변경하는 Update 쿼리문이 나간다. (당연히 트랜잭션 안에서 수행되어야 한다.)

<br>

#### 지연 로딩(Lazy Loading)

객체와 관계형 데이터베이스 매핑하기에서 빛을 발하는데, 연관 관계 매핑되어 있는 엔티티 조회시 프록시를 반환함으로써 쿼리를 진짜 필요할 때 날리는 기능이다. 즉, 불필요한 곳에서는 쿼리를 날리지 않고, 정말로 필요한 경우에만 날리니 서버 부하가 덜 든다.

## References

- [자바 ORM 표준 JPA 프로그래밍 - 기본편](https://www.inflearn.com/course/ORM-JPA-Basic/dashboard)
