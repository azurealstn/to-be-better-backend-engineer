# 즉시로딩과 지연로딩

Member 여러 명이 하나의 Team이 되므로 Member와 Team 일대다의 관계를 갖는다. 여기서 Member를 조회할 때 Team도 같이 조회해야 할까?

## 지연로딩

```java
@Entity
public class Member {
    @Id
    @GeneratedValue
    private Long id;

    @Column(name = "USERNAME")
    private String name;

    @ManyToOne(fetch = FetchType.LAZY) //**
    @JoinColumn(name = "TEAM_ID")
    private Team team;
    ..
}
```

지연 로딩(LAZY)은 LAZY을 사용하여 프록시로 조회한다.

```java
Team team = member.getTeam();
team.getName(); // 실제 Team을 사용하는 시점에 초기화 (DB 조회)
```

실제 Team에서 뭔가를 가져올 때 DB에서 조회하게 된다. 위 코드에서는 `team.getName();`을 통해 Team의 데이터를 가져올 때 DB 쿼리문이 발생하고, Member를 조회할 때는 Team을 조회하는 쿼리문이 발생하지 않는다. DB와의 통신을 줄일 수 있어서 부하를 줄일 수 있다.

## 즉시 로딩

```java
@Entity
public class Member {
    @Id
    @GeneratedValue
    private Long id;

    @Column(name = "USERNAME")
    private String name;

    @ManyToOne(fetch = FetchType.EAGER) //**
    @JoinColumn(name = "TEAM_ID")
    private Team team;
    ..
}
```

즉시 로딩(EAGER)은 Member조회시 항상 Team도 같이 조회한다. 즉, Member를 조회하면 조인을 사용해서 SQL 한번에 함께 조회한다.

### 프록시와 즉시로딩 주의

- 가급적 지연 로딩만 사용한다. (특히 실무에서)
- 즉시 로딩을 적용하면 예상하지 못한 SQL이 발생한다.
- **즉시 로딩은 JPQL에서 N+1 문제를 일으킨다.**
  - JPQL은 SQL로 번역해서 `select * from Member` 로 모든 멤버를 가져온다.
  - Member에 Team 연관관계가 있으면 `select * from Team where TeamId = xxx` 쿼리문이 또 실행된다.
  - 다시 말해, Member를 가져왔는데 2건이 있으면 Team을 가져오는 SQL이 두 번 실행되는 것이다. Member가 10건이 조회되면 Team을 가져오는 SQL이 열 번 실행된다. 지금은 연관관계가 Team 밖에 없어서 그렇지만 다른 테이블도 걸려있다면 훨씬 쿼리문이 많아질 것이다.
  - 이를 해결하기 위해 지연로딩을 사용하는 것이다. 또 다른 방법은 `fetch join` 을 사용한다.
- @ManyToOne, @OneToOne은 기본이 즉시 로딩 -> LAZY로 설정
- @OneToMany, @ManyToMany는 기본이 지연 로딩

## References

- [자바 ORM 표준 JPA 프로그래밍 - 기본편](https://www.inflearn.com/course/ORM-JPA-Basic/dashboard)
