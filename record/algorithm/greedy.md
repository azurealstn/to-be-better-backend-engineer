# 그리디 알고리즘

그리디 알고리즘의 그리디(Greedy)는 탐욕이라는 뜻으로, 말 그대로 미래를 고려하지 않고, 오직 현재 시점에 가장 좋은 선택을 하는 알고리즘이다. 즉, 현재 내가 내린 결정이 나중에 어떤 결과를 낳을지는 고려하지 않고 무조건 지금 가장 저렴한 선택, 가장 빠른 선택 또는 가장 가치 있는 선택을 내리는 것을 말한다.

> ‘각 단계에서 최적이라고 생각되는 것을 선택’ 해 나가는 방식으로 진행하여 최종적인 해답에 도달하는 알고리즘이다. 이때, **항상 최적의 값을 보장하는것이 아니라 최적의 값의 ‘근사한 값’을 목표**로 하고 있다.

## 그리디 조건 & 해결

그리디 알고리즘은 항상 최적 해를 찾아야 하기 때문에 최적 해가 보장되는 조건에서만 그리디 알고리즘을 사용해야 한다.

1. 현재의 선택이 미래의 선택에 영향을 주지 않는다.
2. 하나의 큰 문제들을 작은 문제들로 나눌 수 있고, 작은 문제들에 대한 최적의 해가 더해지는 것이 곧 전체 문제에 대한 최적 해가 되는 구조이다.

위와 같은 조건들을 가지고 그리디 알고리즘을 해결하려면 핵심은 **정렬**이다. 어떻게 정렬해야 미래의 선택은 따져보지 않고, 현재만 고려해도 최적 해를 구할 수 있을까 라는 질문에 대한 답을 찾아야 한다.

## 그리디 예시

그리디 알고리즘의 예시로는 [백준의 5585번: 거스름돈](https://www.acmicpc.net/problem/5585) 문제가 있다. 문제는 잔돈들이 있고, 언제나 거스름돈 개수가 가장 적게 잔돈을 줬을 때 잔돈의 개수를 구하는 것이다. (카운터에서 지페 1000엔을 지불한다.)

```java
import java.util.*;
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());

        int change = 1000 - n; // 타로에게 줘야할 잔돈
        int result = 0; // 최소의 잔돈 개수
        int[] money = {500, 100, 50, 10, 5, 1}; // 잔돈의 종류들
        int i = 0; // 500엔부터 시작
        while (change != 0) {
            // 잔돈의 종류중에서 잔돈을 줄 수 있는 경우
            if (change - money[i] >= 0) {
                change -= money[i];
                result++;
            } else { // 잔돈의 종류중에서 잔돈을 줄 수 없는 경우
                i++;
            }
        }

        System.out.println(result);

    }
}
```

## References

- [개발자로 취직하기 - 그리디 알고리즘](https://www.youtube.com/watch?v=_IZuE7NIeW4)
- https://adjh54.tistory.com/212
- https://propercoding.tistory.com/204
