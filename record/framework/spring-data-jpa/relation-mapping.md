# 연관관계 매핑

기본적인 개념 정도만 다루고, 자세한 연관관계에 대한 설명은 [자바 ORM 표준 JPA 프로그래밍 - 기본편](https://www.inflearn.com/course/ORM-JPA-Basic/dashboard)이나 책을 참고하시면 좋을 것 같다.

## 단방향 연관관계

```java
@Entity
public class Member {

    @Id @GeneratedValue
    private Long id;

    @Column(name = "USERNAME")
    private String name;
    private int age;

    // @Column(name = "TEAM_ID")
    // private Long teamId;

    @ManyToOne
    @JoinColumn(name = "TEAM_ID")
    private Team team;

    …
}
```

- `@ManyToOne`: 외래 키 매핑 (항상 일대다에서 다쪽에 걸어야 한다. 왜냐하면 외래 키는 다쪽에 있으니까!)
- `@JoinColumn(name = "TEAM_ID")`: 외래 키명을 지정할 수 있다.

## 양방향 연관관계

양방향 연관관계에서는 연관관계의 주인을 정해야 한다. 양방향 연관관계는 연관관계를 일대다에서 일에도 설정하고 다에도 설정하는 것을 말한다. (다에는 `@ManyToOne`을 사용하여 연관관계를 맺고, 일에는 `@OneToMany`을 사용하여 연관관계를 맺는다.)

즉, 양방향 연관관계는 객체의 양방향 관계는 사실 양방향 관계가 아니라 서로 다른 단뱡향 관계 2개다.

```java
@Entity
public class Team {

    @Id @GeneratedValue
    private Long id;
    private String name;

    @OneToMany(mappedBy = "team")
    List<Member> members = new ArrayList<Member>();
    …
}
```

- `@OneToMany(mappedBy = "team")`: 양방향 연관관계가 성립된다. 양방향 연관관계에서는 주인을 정해야 한다.

### 연관관계의 주인(Owner)

- 객체의 두 관계중 하나를 연관관계의 주인으로 지정한다.
- **연관관계의 주인만이 외래 키를 관리(등록, 수정)**할 수 있다.
- **주인이 아닌쪽은 읽기만 가능**하다.
- 주인은 mappedBy 속성 사용X - mappedBy 속성을 사용했다는건 뭐에 의해서 매핑이 되었다는 뜻이므로 내가 주인이 아니라는 뜻이다. (즉, 위 코드는 Team이 아닌 Member가 연관관계의 주인이 된다.)
- 주인이 아니면 mappedBy 속성으로 주인 지정한다.

객체의 두 관계중 하나를 연관관계의 주인으로 지정할 수 있다고 했는데 어느쪽을 주인으로 정해야 할까?

#### 외래 키가 있는 있는 곳을 주인으로 정해라

- 다대일 관계에서 다를 주인으로 정해라.
- 다대일 관계에서 다는 외래 키가 있는 곳이다.
- 이유는 외래 키가 없는 Team을 Update했는데 갑자기 Member가 Update 되는 상황이 발생한다.
- 잘 생각해보면 Member에 외래키가 있고, Team이 있다. 즉, Member를 Update할 떄는 Team이 Update되도 상관없는 것이다. Member에 외래키가 있기 때문이다.

### 양방향 연관관계 주의

- 순수 객체 상태를 고려해서 항상 양쪽에 값을 설정하자.
- 연관관계 편의 메소드를 생성하자.
  - 편의 메소드는 둘 중에 한 곳에만 사용하자
- 양방향 매핑시에 무한 루프를 조심하자
  - 예: toString(), lombok, JSON 생성 라이브러리
  - 양방향 관계에서 양쪽에 toString()을 만들게 되면 서로 toString()을 무한으로 찍는다.
    - lombok 에서 toString()을 지양하자.
    - JSON 생성 라이브러리는 컨트롤러에서 Entity를 반환하면 양방향 관계에서 서로 JSON으로 변환하는중에 무한 루프에 빠질 수 있다.
    - 결론은 컨트롤러에서는 Entity를 절대로 반환하지 말자. (반환 DTO를 만들어서 반환하자. 이것만 해결해도 문제의 대부분을 해결할 수 있다.)
      - 무한 루프에서 해결될 수 있다.
      - API 스펙이 변경되면 영향이 끼친다.

## 실무팁

정답은 없지만 [제미니의 개발실무 - 연관관계](https://www.youtube.com/watch?v=vgNHW_nb2mg&t=180s) 영상을 보면서 정리했다.

- 애초에 연관관계 거의 걸지 않는다.
- id로만 매핑을 하고, FK(외래키)는 쓰지 않는다. (상황에 따라 달라질 수 있다.)
  - reviewEntity(1) : reviewImageEntity(N)
  - 위 관계에서 reviewImageEntity에 reviewId 컬럼만 둔다.
- 양방향 연관관계를 걸지 않는다.
- 단방향만 걸고, `@OneToMany`, `@OneToOne`은 안건다.

## References

- [자바 ORM 표준 JPA 프로그래밍 - 기본편](https://www.inflearn.com/course/ORM-JPA-Basic/dashboard)
- [제미니의 개발실무 - 연관관계](https://www.youtube.com/watch?v=vgNHW_nb2mg&t=180s)
