# To Be Better Backend Engineer

이 레포지토리는 더 나은 백엔드 엔지니어가 되기 위해 공부한 내용을 기록하기 위한 목적으로 만들었습니다.

## Git & GitHub

- [BOOK] [모두의 깃 & 깃허브](/book/git-for-everyone/readme.md)

<br>
<br>
<br>

## Database

- [BOOK] [SQL 첫걸음](/book/sql-first-step/readme.md)

<br>
<br>
<br>

## Network

- [BOOK] [그림으로 배우는 Http & NetWork Basic](/book/http_network_basic/readme.md)
- [OSI 7 계층](/record/network/OSI%207%20계층.md)
- [IP](/record/network/ip.md)
- [TCP/IP](/record/network/tcp_ip.md)
- [TCP와 UDP](/record/network/tcp-udp.md)
- [TCP 3, 4 way handshake](/record/network/3-4-way-handshake.md)
- [DNS](/record/network/dns.md)
- [URI, URL, URN](/record/network/uri.md)
- [웹 브라우저 요청 흐름: https://www.google.com 에 접속하면 일어나는 일](/record/network/웹_브라우저_요청_흐름.md)
- [HTTP](/record/network/http.md)
- [HTTP 메시지](/record/network/http-message.md)
- [HTTP 메서드](/record/network/http-method.md)
  - GET vs POST
  - PUT vs PATCH
  - 속성 (안전, 멱등)
- [REST API](/record/network/rest_api.md)
- [컬렉션, 스토어](/record/network/컬렉션.스토어.md)
- [HTTP 상태코드](/record/network/http-status-code.md)
- [HTTP 헤더](/record/network/http-header.md)
  - 표현 헤더
  - 컨텐츠 협상
  - 일반 정보(referer, user-agent..)
  - 특별한 정보(Host, Location..)
  - 인증
- [쿠키와 세션](/record/network/cookie-session.md)
- [캐시](/record/network/cache.md)
- [검증 헤더와 조건부 요청](/record/network/valid-cache.md)
- [캐시 헤더](/record/network/cache-control.md)
- [프록시 캐시](/record/network/proxy-cache.md)

<br>
<br>
<br>

## Computer Architecture

- [BOOK] [혼자 공부하는 컴퓨터 구조와 운영체제](/book/os-for-self-study/computer-structure.md)
  - 컴퓨터 구조 파트

<br>
<br>
<br>

## Operation System

- [BOOK] [혼자 공부하는 컴퓨터 구조와 운영체제](/book/os-for-self-study/operating-system.md)
  - 운영체제 파트

<br>
<br>
<br>

## Data Structure & Algorithm

자료구조란 데이터 단위와 데이터 자체 사이의 물리적 또는 논리적인 관계를 말한다. 여기서 데이터 단위는 데이터를 구성하는 하나의 덩어리라고 생각하면 된다. 쉽게 말해 자료구조는 자료를 효율적으로 사용할 수 있도록 컴퓨터에 저장하는 방법을 말한다.

자료구조의 분류는 크게 2가지로 나뉜다.

- 선형 구조 (Linear): 자료를 구성하는 원소들을 하나씩 순차적으로 나열시킨 형태
- 비선형 구조 (NonLinear): 하나의 자료 뒤에 여러개의 자료가 존재할 수 있는 형태

![data-structure-1](/images/data-structure-1.png)
(사진 출처: https://jud00.tistory.com/entry/Data-Structure-%EC%84%A0%ED%98%95Linear-%EB%B9%84%EC%84%A0%ED%98%95NonLinear-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0)

#### 자료구조와 알고리즘의 차이는 무엇일까?

자료구조는 데이터를 상황에 맞게 저장하기 위한 구조이고, 일고리즘은 자료구조에 있는 데이터를 활용해 어떠한 문제를 해결하기 위한 여러 방법들의 모임이라고 볼 수 있다.

### 자료구조

- [배열(Array)과 리스트(List)](/record/data-structure/array-list.md)
- [스택(Stack)](https://azurealstn.tistory.com/37)
- [큐(Queue)](https://azurealstn.tistory.com/38)
- [덱(Deque)](https://azurealstn.tistory.com/151)
- [해시테이블(Hash Table)](https://azurealstn.tistory.com/146)
- [트리(Tree)](https://azurealstn.tistory.com/143)
- [힙(Heap)](https://azurealstn.tistory.com/144)
- [우선순위 큐(Priority Queue)](https://azurealstn.tistory.com/158)
- [그래프(Graph)](https://azurealstn.tistory.com/145)
- [AVL Tree](https://azurealstn.tistory.com/153)
- [Red-Black Tree](https://azurealstn.tistory.com/154)
- [B-Tree](https://azurealstn.tistory.com/155)

### 알고리즘

- [선택정렬(Selection Sort)](https://azurealstn.tistory.com/156)
- [삽입정렬(Insertion Sort)](https://azurealstn.tistory.com/157)
- [버블정렬(Bubble Sort)](https://azurealstn.tistory.com/29)
- [퀵정렬(Quick Sort)](https://azurealstn.tistory.com/149)
- [병합정렬(Merge Sort)](https://azurealstn.tistory.com/34)
- [힙정렬(Heap Sort)](https://azurealstn.tistory.com/159)
- [이분 탐색(Binary Search)](/record/algorithm/binary-search.md)
- [브루트 포스(Brute Force)](/record/algorithm/brute-force.md)
- [에라토스테네스의 체](/record/algorithm/eratos.md)
- [Two pointers, Sliding window](/record/algorithm/two-p-sliding-w.md)
- [DFS, BFS 구현](/record/algorithm/dfs-bfs.md)
- [그리디(Greedy)](/record/algorithm/greedy.md)
- [다익스트라(Dijkstra)](/record/algorithm/dijkstra.md)
- [Union & Find](/record/algorithm/union-find.md)
- [최소 스패닝 트리(MST)](/record/algorithm/mst.md)
- [동적 프로그래밍(Dynamic Programming)](/record/algorithm/dp.md)
- [유클리드 호제법](/record/algorithm/Euclidean.md)

<br>
<br>
<br>

## Java

- [JVM이란?](https://azurealstn.tistory.com/136)
- [변수 초기화](/record/language/java/variable-init.md)
- [스코프](/record/language/java/scope.md)
- [기본형과 참조형](/record/language/java/primitive-reference.md)
- [Call by Value와 Call By Reference](/record/language/java/call-by-value.md)
- [형변환](/record/language/java/type-casting.md)
- [클래스 - 생성자](/record/language/java/class.md)
- [접근제어자 - 캡슐화](/record/language/java/access-modifier.md)
- [자바 메모리 구조 - static](/record/language/java/java-memory.md)
- [final](/record/language/java/final.md)
- [오버로딩과 오버라이딩](/record/language/java/overloading-overriding.md)
- [추상클래스와 인터페이스](/record/language/java/abstract-interface.md)

<br>
<br>
<br>

## Spring

- [스프링 IoC, DI, SOLID](https://azurealstn.tistory.com/126)
- [싱글톤 컨테이너](/record/framework/spring/singleton.md)
- [컴포넌트 스캔](/record/framework/spring/componentscan.md)
- [생성자 주입](https://azurealstn.tistory.com/135)
- [빈 생명주기](/record/framework/spring/bean-lifecycle.md)
- [서블릿](https://azurealstn.tistory.com/137)
- [Spring MVC](https://azurealstn.tistory.com/138)
- [@RequestParam과 @ModelAttribute](https://azurealstn.tistory.com/139)
- [HttpEntity, @RequestBody, @ResponseBody](https://azurealstn.tistory.com/140)

<br>
<br>
<br>

## Spring Data JPA

- [영속성 컨텍스트](/record/framework/spring-data-jpa/persistence.md)
- [엔티티 매핑](/record/framework/spring-data-jpa/entity-mapping.md)
- [연관관계 매핑](/record/framework/spring-data-jpa/relation-mapping.md)
- [즉시로딩과 지연로딩](/record/framework/spring-data-jpa/eager-lazy.md)
- [OSIV](/record/framework/spring-data-jpa/osiv.md)
- [N + 1 문제](/record/framework/spring-data-jpa/n+1.md)
