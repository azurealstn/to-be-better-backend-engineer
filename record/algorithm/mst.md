# 최소 스패닝 트리 (MST: Minimum Spanning Tree)

스패닝 트리란, 신장 트리로 그래프의 모든 정점을 잇지만 사이클이 없는 부분 그래프를 의미한다.

최소 스패닝 트리는 사이클 없이 가능한 최소 총 간선 가중치를 사용하여 모든 정점을 함께 연결하는 연결된 간선 가중치 무방향 그래프 간선의 하위 집합이다. 즉, 간선 가중치의 합이 최대한 작은 스패닝 트리를 말한다. 여기서 포인트는 무방향 그래프라는 점이다.

여기서 포인트는 무방향 그래프라는 점과 그래프의 하위 집합은 사이클이 없다는 점에서 트리의 특징을 가지고 있다. (사이클이 있으면 그래프, 사이클이 없으면 트리)

![Minimum_spanning_tree](/record/algorithm/images/Minimum_spanning_tree.svg)
(출처: https://commons.wikimedia.org/wiki/File:Minimum_spanning_tree.svg#/media/File:Minimum_spanning_tree.svg)

위 그림을 보면 모든 정점을 이으면서 간선 가중치의 합이 최소인 부분이 검은색 간선이다.

## MST 특징

- 간선의 가중치의 합이 최소여야 한다.
- n개의 정점을 가지는 그래프에 대해 반드시 (n-1)개의 간선만을 사용해야 한다.
- 사이클이 포함되어서는 안된다.

## MST 사용 사례

통신망, 도로망, 유통망에서 길이, 구축 비용, 전송 시간 등을 최소로 구축하려는 경우

- 도로 건설
  - 도시들을 모두 연결하면서 도로의 길이가 최소가 되도록 하는 문제
- 전기 회로
  - 단자들을 모두 연결하면서 전선의 길이가 가장 최소가 되도록 하는 문제
- 통신
  - 전화선의 길이가 최소가 되도록 전화 케이블 망을 구성하는 문제
- 배관
  - 파이프를 모두 연결하면서 파이프의 총 길이가 최소가 되도록 연결하는 문제

## MST 구현

최소 스패닝 트리를 구현하는 방법에는 2가지 알고리즘이 있다.

- 크루스칼(Kruskal)
- 프림(Prim)

최소 스패닝 트리의 예제로는 백준의 [1197번: 최소 스패닝 트리](https://www.acmicpc.net/problem/1197) 문제로 코드를 구현해보겠다.

### 크루스칼(Kruskal) 알고리즘

크루스칼은 그리디 알고리즘을 이용하여 네트워크(가중치를 간선에 할당한 그래프)의 모든 정점을 최소 비용으로 연결하는 최적의 해를 구하는 것이다.

- 각 단계마다 사이클을 이루지 않는 최소 비용 간선을 선택한다.
- 간선 선택을 기반으로 하는 알고리즘이다. 여기서 Union & Find 알고리즘을 사용한다. 두 정점을 이은 간선이 선택되면 Union으로 합쳐야 한다.
- 이전 단계에서 만들어진 스패닝 트리와는 상관없이 무조건 최소 간선만을 선택하는 방법이다.

#### 과정

1. 가중치 값을 기준으로 오름차순 정렬한다.
2. 정렬된 간선 리스트에서 순서대로 사이클을 형성하지 않는 간선을 선택한다. 이 때 가장 작은 가중치를 먼저 선택한다.
3. 선택된 간선을 집합에 추가한다.

```java
import java.util.*;
import java.io.*;

class Edge implements Comparable<Edge> {
    int v1;
    int v2;
    int cost;

    public Edge(int v1, int v2, int cost) {
        this.v1 = v1;
        this.v2 = v2;
        this.cost = cost;
    }

    @Override
    public int compareTo(Edge o) {
        return cost - o.cost;
    }
}
public class Main {
    static int[] unf;

    private static int find(int v) {
        if (v == unf[v]) return v;
        return unf[v] = find(unf[v]);
    }

    private static void union(int a, int b) {
        int fa = find(a);
        int fb = find(b);
        if (fa != fb) {
            unf[fa] = fb;
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        st = new StringTokenizer(br.readLine());
        int v = Integer.parseInt(st.nextToken()); // 정점의 개수
        int e = Integer.parseInt(st.nextToken()); // 간선의 개수
        unf = new int[v + 1];
        ArrayList<Edge> list = new ArrayList<>();
        for (int i = 1; i <= v; i++) {
            unf[i] = i;
        }

        for (int i = 0; i < e; i++) {
            st = new StringTokenizer(br.readLine());
            int v1 = Integer.parseInt(st.nextToken());
            int v2 = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());
            list.add(new Edge(v1, v2, cost));
        }

        Collections.sort(list);
        int result = 0; // 최소 스패닝 트리의 가중치 값

        for (Edge o : list) {
            int fv1 = find(o.v1);
            int fv2 = find(o.v2);

            // 두 정점을 find로 찾은 다음 값이 다르면 간선이 선택된다.
            if (fv1 != fv2) {
                result += o.cost;

                // 간선이 선택되면 간선을 합친다.
                union(o.v1, o.v2);
            }
        }

        System.out.println(result);

    }
}
```

### 프림(Prim) 알고리즘

시작 정점에서부터 출발하여 신장트리 집합을 단계적으로 확장 해나가는 방법이다.

- 정점 선택을 기반으로 하는 알고리즘이다. 여기서 프림은 우선순위 큐(Priority Queue) 알고리즘을 사용한다.
- 이전 단계에서 만들어진 신장 트리를 확장하는 방법이다.

#### 과정

1. 시작 단계에서는 시작 정점만이 MST(최소 비용 신장 트리) 집합에 포함된다.
2. 앞 단계에서 만들어진 MST 집합에 인접한 정점들 중에서 최소 간선으로 연결된 정점을 선택하여 트리를 확장한다. (인접리스트 사용, 무방향 그래프)
   - 체크 배열을 만들어서 방문한 노드는 재방문이 안되고, 방문한 노드의 인접한 노드들을 우선순위 큐에 넣는다.
3. 위의 과정을 트리가 (N-1)개의 간선을 가질 때까지 반복한다.

```java
import java.util.*;
import java.io.*;

class Edge implements Comparable<Edge> {
    int v;
    int cost;

    public Edge(int v, int cost) {
        this.v = v;
        this.cost = cost;
    }

    @Override
    public int compareTo(Edge o) {
        return cost - o.cost;
    }
}
public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        st = new StringTokenizer(br.readLine());
        int v = Integer.parseInt(st.nextToken()); // 정점의 개수
        int e = Integer.parseInt(st.nextToken()); // 간선의 개수
        ArrayList<ArrayList<Edge>> graph = new ArrayList<>();

        // 각 정점마다 인접 리스트 초기화
        for (int i = 0; i <= v; i++) {
            graph.add(new ArrayList<>());
        }

        // 재방문하지 않기 위한 체크 배열
        int[] ch = new int[v + 1];
        for (int i = 0; i < e; i++) {
            st = new StringTokenizer(br.readLine());
            int v1 = Integer.parseInt(st.nextToken());
            int v2 = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());

            // 무방향 그래프이기 때문에 두 방향에 대해 값을 설정한다.
            graph.get(v1).add(new Edge(v2, cost));
            graph.get(v2).add(new Edge(v1, cost));
        }

        int result = 0; // 최소 스패닝 트리의 가중치 값
        PriorityQueue<Edge> pQ = new PriorityQueue<>();

        // 시작 정점 포함
        pQ.offer(new Edge(1, 0));
        while (!pQ.isEmpty()) {
            Edge cur = pQ.poll();
            int cv = cur.v;
            int cc = cur.cost;

            // 방문하지 않은 경우
            if (ch[cv] == 0) {
                ch[cv] = 1;
                result += cc;
                // 인접한 정점들을 선택한다.
                for (Edge o : graph.get(cv)) {
                    // 인접한 정점들이 방문하지 않은 경우
                    if (ch[o.v] == 0) {
                        pQ.offer(new Edge(o.v, o.cost));
                    }
                }
            }
        }

        System.out.println(result);

    }
}
```

## Referneces

- [자바(Java) 알고리즘 문제풀이 입문: 코딩테스트 대비](https://www.inflearn.com/course/%EC%9E%90%EB%B0%94-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%ED%85%8C%EB%8C%80%EB%B9%84/dashboard)
- https://gmlwjd9405.github.io/2018/08/28/algorithm-mst.html
- https://en.wikipedia.org/wiki/Minimum_spanning_tree
