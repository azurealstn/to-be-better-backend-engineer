# Union & Find

Union & Find 는 대표적인 그래프 알고리즘이며, 합집합 찾기라는 의미를 가진 알고리즘이다. 또한 서로소 집합(Disjoint-Set) 알고리즘이라고도 부른다.

Union & Find 는 여러 노드가 존재할 때, 두 개의 노드를 선택해서 현재 두 노드가 서로 같은 그래프에 속하는지 판별하는 알고리즘이다.

> 서로소 집합이란, 두 집합이 서로 공통 원소가 없는 경우 그 두 집합은 서로소 집합이라고 한다.

2가지 연산으로 이루어져 있다.

- Find: x가 어떤 집합에 포함되어 있는지 찾는 연산
- Union: x와 y가 포함되어 있는 집합을 합치는 연산

Union & Find 알고리즘은 최소 스패닝 트리 - 크루스칼 알고리즘에 활용되므로 개념 정보는 익혀두자.

## 예제 문제

Union & Find의 대표적인 예제 문제로는 백준의 [1717번: 집합의 표현](https://www.acmicpc.net/problem/1717) 문제가 있다. Union & Find는 문제는 Union으로 합집합 연산을 하고, Find로 원소를 찾는 그런 작업을 수행한다.

집합의 표현 문제 역시 두 원소가 같은 집합에 포함되 있는지를 확인하는 문제로써, 이는 달리 말해 두 개의 노드를 선택해서 현재 두 노드가 서로 같은 그래프에 속하는지 판별하는 알고리즘이다. 여기서는 포함되어 있으면 "YES"를 아니면 "NO"를 출력한다.

그리고 문제의 입력에서 (0, a, b)처럼 0일 경우 (a, b)의 합집합을 연산하고, (1, a, b)처럼 1일 경우 (a, b)의 교집합 즉, 같은 집합에 포함되어 있는지 여부를 확인하면 된다.

### 코드보기

```java
import java.util.*;
import java.io.*;

public class Main {
    static int[] unf;

    private static int find(int v) {
        if (v == unf[v]) {
            return v;
        }
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
        int n = Integer.parseInt(st.nextToken()); // 0부터 n까지의 숫자
        int m = Integer.parseInt(st.nextToken()); // m개의 연산

        // unf 배열을 1번부터 n까지 숫자로 초기화한다.
        unf = new int[n + 1];
        for (int i = 1; i <= n; i++) {
            unf[i] = i;
        }

        // m개의 연산 반복
        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int op = Integer.parseInt(st.nextToken());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            // op가 0인 경우 합집합 연산
            if (op == 0) {
                // a와 b를 합집합 연산
                union(a, b);
            }

            // op가 1인 경우 같은 집합에 포함되어 있는지 확인
            if (op == 1) {
                int fa = find(a);
                int fb = find(b);

                // find 메서드를 사용하여 두 원소를 찾아서 교집합인지 확인한다.
                if (fa == fb) {
                    System.out.println("YES");
                } else {
                    System.out.println("NO");
                }
            }
        }

    }
}
```

Union & Find 문제는 그냥 메서드 자체를 외워버리는 게 낫다. 동작 방식에 대해 궁금하다면 나동빈님의 [합집합 찾기](https://www.youtube.com/watch?v=AMByrd53PHM&t=115s) 영상이 있으니 참고하는 것도 좋다.

## References

- https://brenden.tistory.com/33
- [자바(Java) 알고리즘 문제풀이 입문: 코딩테스트 대비](https://www.inflearn.com/course/%EC%9E%90%EB%B0%94-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%ED%85%8C%EB%8C%80%EB%B9%84/dashboard)
