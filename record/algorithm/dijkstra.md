# 다익스트라(Dijkstra) 알고리즘

다익스트라(Dijkstra) 알고리즘은 도로 교통망 같은 곳에서 나타날 수 있는 그래프에서 꼭짓점 간의 **최단 경로를 찾는 알고리즘**이다. 또한 특정한 하나의 정점에서 다른 정점으로 가는 최단 경로를 찾는다.

#### 아래의 경우 다익스트라를 활용한다.

- 한 정점에서 다른 한 정점까지의 최단 경로
- 한 정점에서 다른 모든 정점까지의 최단 경로
- 모든 정점에서 다른 모든 정점까지의 최단 경로

여기서 각 정점은 노드로 표현하고, 정점 간 연결된 선은 간선으로 표현한다. 참고로 다익스트라 알고리즘은 가중치 방향그래프에서 활용될 수 있고, 가중치의 값은 절대로 음수값이 나올 수 없다. 또한 다익스트라 알고리즘은 매번 최단 경로 찾는 즉, 최적의 해를 찾는 과정을 거쳐 그리디 알고리즘으로 분류된다.

## 동작 과정

1. 출발 노드를 설정한다.
2. 최단 거리 테이블을 초기화한다.
3. 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택한다. -> 여기서 기본적으로 그리디 알고리즘을 활용하고 있는 것을 확인할 수 있다.
4. 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신한다.
5. 3번과 4번 과정을 반복한다.

![dijkstra-1](https://github.com/azurealstn/to-be-better-backend-engineer/assets/55525868/17dbd56d-16c8-4ff2-ba1a-0938419dce0c)

먼저 위와 같은 가중치 방향그래프가 있을 때 한 정점에서 다른 모든 정점까지의 최단 경로를 구해볼 것이다. 출발 노드는 `1`번 노드로 설정하고, 최단 거리 테이블은 배열 형태로 `int`형의 MAX 값으로 초기화해주었다. 그리고 배열의 인덱스는 노드의 번호로 나타낸다.

![dijkstra-2](https://github.com/azurealstn/to-be-better-backend-engineer/assets/55525868/7b07a862-965c-4d28-a17c-400ccf820e6f)

`1`번 노드부터 출발하므로 dis 배열의 1번 인덱스에 0으로 변경한다. 변경 후 dis 배열을 `O(N)`으로 쭈욱 탐색해서 최솟값을 찾는다. (최솟값은 최단 경로를 의미한다.) 여기서는 1번 노드의 값인 0이 가장 작으므로 1번 인덱스에 방문했다고 체크해준다.

![dijkstra-3](https://github.com/azurealstn/to-be-better-backend-engineer/assets/55525868/a83b778e-a9a3-4eb6-88ac-69a864b1c15c)

다음으로 1번 노드에서 갈 수 있는 노드는 3번 노드이며, 가중치의 값인 4는 3번 인덱스의 값인 M(Max)보다 작으므로 스왑(swap)해준다. dis 배열을 `O(N)`으로 쭈욱 탐색해서 최솟값을 찾는다. 이번에는 3번 노드가 가장 작으므로 3번 인덱스에 방문했다고 체크해준다. (한번 방문한 노드는 또 방문하지 않는다.)

> 참고로 여기서 방문했다고 체크해준 노드들은 확정이 된 노드들이다. 즉, 해당 정점으로 가는 최단 거리(최적의 해)가 구해진 것이다.

![dijkstra-4](https://github.com/azurealstn/to-be-better-backend-engineer/assets/55525868/75b1815a-496c-4e02-b429-4565554b85c2)

다음으로 3번 노드에서 갈 수 있는 노드는 4번 노드이며, 1번 노드에서 4번 노드까지의 거리는 `4 + 5 = 9`가 된다. 따라서 4번 인덱스값인 M(Max)보다 작으므로 9를 할당한다. 그리고 dis 배열을 탐색해서 최솟값이 9가 되므로 방문 체크해준다.

현재까지는 1번, 3번, 4번까지의 최단 거리를 구한 셈이다.

![dijkstra-5](https://github.com/azurealstn/to-be-better-backend-engineer/assets/55525868/ef2e9736-4ad0-4c81-b8fb-799d54b1ebdc)

다음으로 4번 노드에서 갈 수 있는 2번 노드까지의 거리는 `9 + 2 = 11`이고, dis 배열의 값을 갱신한다. 또 4번 노드에서 갈 수 있는 6번 노드까지의 거리는 `9 + 11 = 20`이므로 dis 배열의 값을 갱신한다. 갱신을 모두 완료했으면 다시 dis 배열을 탐색해서 최소값을 구한다. 이번에는 2번 인덱스가 가장 작으므로 방문 체크한다.

![dijkstra-6](https://github.com/azurealstn/to-be-better-backend-engineer/assets/55525868/5dd78c6c-5725-422f-927b-f23d41827a16)

다음으로 2번 노드에서 갈 수 있는 노드는 1번 노드와 5번 노드가 있는데 1번 노드는 이미 방문했으므로 넘어가고, 5번 노드를 갱신한다. `11 + 6 = 17`로 갱신하면 되겠다. 그리고 방문 체크해준다.

![dijkstra-7](https://github.com/azurealstn/to-be-better-backend-engineer/assets/55525868/74379a3e-ad26-42a3-88c8-1a9b5b18e237)

마지막으로 5번 노드에서 갈 수 있는 노드는 6번 노드가 있고, `17 + 3 = 20` 이므로 갱신하지 않는다. 기존 dis 배열의 값보다 작은 경우에만 갱신하기 때문이다. 따라서 그대로 두고, 방문 체크해준다.

지금까지 1번 정점에서 다른 모든 정점까지의 최단 경로를 구했다.

하지만 위 방식은 정점의 개수가 N개 있을 때 dis 배열을 N번 돌아야 하므로 시간복잡도가 `O(N^2)`이 걸린다. 이를 개선하기 위해 **PriorityQueue 자료구조**를 사용하면 `O(N logN)`으로 시간복잡도를 줄일 수 있다. dis 배열에서 탐색할 때 PriorityQueue를 이용하게 `O(log N)`으로 최솟값을 찾으면 훨씬 빠르게 찾을 수 있다.

### 코드보기

```java
import java.util.*;
import java.io.*;

class Edge implements Comparable<Edge> {
    int vex; // 정점 (노드)
    int cost; // 비용 (가중치)

    public Edge(int vex, int cost) {
        this.vex = vex;
        this.cost = cost;
    }

    // 최소값을 꺼내기 위해 오름차순 정렬한다.
    @Override
    public int compareTo(Edge o) {
        return cost - o.cost;
    }
}
public class Main {
    // n: 정점의 개수
    // m: 방향 그래프를 나타내는 개수
    static int n, m;
    static ArrayList<ArrayList<Edge>> graph; // 가중치 방향 그래프
    static int[] dis; // 최단거리 dis 배열

    private static void solution(int v) {
        // 최소값을 꺼내기 위해 우선순위 큐 자료구조 사용
        PriorityQueue<Edge> pQ = new PriorityQueue<>();

        // 가장 먼저 1번 정점의 우선순위 큐에 넣는다.
        pQ.offer(new Edge(v, 0));

        // dis 배열의 1번 인덱스 0으로 변경
        dis[v] = 0;
        while (!pQ.isEmpty()) {
            // 우선순위 큐에 의해 가장 작은 비용이 빠져나온다.
            Edge cur = pQ.poll();
            int cv = cur.vex; // 현재 정점
            int cc = cur.cost; // 현재 비용

            // 현재 비용(거리)이 dis 배열에 있는 값보다 크면 그냥 넘어간다.
            // 이 경우는 최적의 해가 아니기 때문에 넘어가는 것이다.
            if (cc > dis[cv]) continue;

            // 현재 정점에서 갈 수 있는 노드들 반복
            for (Edge o : graph.get(cv)) {
                // dis 배열에 있는 값이 해당 노드까지의 거리보다 큰 경우
                // ex. 1번 노드에서 4번 노드까지의 거리는 `4 + 5 = 9`가 된다.
                if (dis[o.vex] > cc + o.cost) {
                    // dis 배열에서 해당 노드의 인덱스 값을 갱신한다.
                    dis[o.vex] = cc + o.cost;

                    // pQ에 해당 노드의 정점과 비용을 넣고, 방문 체크된다.
                    pQ.offer(new Edge(o.vex, cc + o.cost));
                }
            }
        }
    }
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        // 그래프의 인접리스트를 이용하여 각 정점이 갈 수 있는 노드들을 ArrayList로 표현했다.
        // 아래 코드는 각 정점마다 new ArrayList<>()로 초기화 하였다.
        // 1번 정점부터 시작하므로 n까지 루프를 돌아야한다.
        graph = new ArrayList<>();
        for (int i = 0; i <= n; i++) {
            graph.add(new ArrayList<>());
        }

        // dis 배열 역시 1번 인덱스부터 시작하므로 n+1만큼 크기를 선언한다.
        dis = new int[n + 1];

        // dis 배열을 모두 MAX값으로 초기화한다.
        Arrays.fill(dis, Integer.MAX_VALUE);

        // m번 만큼 돌아서 가중치 방향 그래프를 나타낸다.
        for (int i = 0; i < m; i++) {
            // a -> b 로 갈 수 있으며, 비용이 c 이다.
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());
            // a 정점에서 b로 갈 수 있으며, c 비용이 든다.
            // 이 부분이 이해가 안간다면 그래프의 인접리스트를 공부해야 한다.
            graph.get(a).add(new Edge(b, c));
        }
        // 1번 정점부터 설정
        solution(1);

        // 1번 정점에서 각 정점들까지의 최단 거리를 출력한다.
        // 갈 수 없는 경우에도 출력한다.
        for (int i = 2; i <= n; i++) {
            if (dis[i] != Integer.MAX_VALUE) {
                System.out.println(i + " : " + dis[i]);
            } else {
                System.out.println(i + " : " + "갈 수 없어요 ㅠ..");
            }
        }
    }
}
```

#### 출력 결과

```java
2 : 11
3 : 4
4 : 9
5 : 17
6 : 20
```

<br>

## References

- [자바(Java) 알고리즘 문제풀이 입문: 코딩테스트 대비](https://www.inflearn.com/course/%EC%9E%90%EB%B0%94-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%ED%85%8C%EB%8C%80%EB%B9%84/dashboard)
- [(이코테 2021 강의 몰아보기) 7. 최단 경로 알고리즘](https://www.youtube.com/watch?v=acqm9mM1P6o)
