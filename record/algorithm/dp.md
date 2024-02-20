# 다이나믹 프로그래밍

다이나믹 프로그래밍(Dynamic Programming)은 동적 계획법이라고도 불리며, 다이나믹 프로그래밍의 다이나믹은 별다른 의미 없이 사용된 단어이다.

다이나믹 프로그래밍은 완전 탐색, DFS, BFS와 같이 수많은 경우의 수를 전부 따져봐야 하는데 그 경우가 너무 많아서 속도가 느려지는 문제를 개선하고자 즉, 수행 시간을 단축하고자 만들어진 알고리즘이다.

## 다이나믹 프로그래밍 특징

- 다이나믹 프로그래밍은 메모리를 적절히 사용하여 수행 시간 효율성을 향상시키는 방법이다.
- 이미 계산된 결과(작은 문제)는 별도의 메모리 영역에 저장하여 다시 계산하지 않도록 한다.

## 다이나믹 프로그래밍 조건

다이나믹 프로그래밍은 다음 조건을 만족할 때 사용할 수 있다.

- 최적 부분 구조 (Optimal Substructure)
  - 큰 문제를 작은 문제로 나눌 수 있으며 작은 문제의 답을 모아서 큰 문제를 해결할 수 있다.
- 중복되는 부분 문제 (Overlapping Subproblem)
  - 동일한 작은 문제를 반복적으로 해결해야 한다.

### 다이나믹 프로그래밍 예제

다이나믹 프로그래밍이 여러운 이유는 특정 유형에만 국한되지 않고, 다양한 유형의 문제를 최적화할 때 고려될 수 있는 알고리즘이다. 그럼 문제를 보고 어떨때 다이나믹 프로그래밍으로 풀어야 하는지 알 수 있을까?

- DFS/BFS로 풀 수는 있지만 경우의 수가 너무 많은 문제
- 경우의 수들에 중복적인 연산이 많은 경우
- DP 문제들을 최대한 많이 풀어본다..(ㅠㅠ)

다이나믹 프로그래밍 문제의 예제로는 백준의 [2579번: 계단 오르기](https://www.acmicpc.net/problem/2579) 문제가 있다. 코드를 보면 "아, 이런게 다이나믹 프로그래밍이구나~" 하고 이해할 수 있다.

```java
import java.util.*;
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int[] arr = new int[n + 1];
        for (int i = 1; i <= n; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }
        // 메모리를 사용하여 효울성 증가
        int[] dp = new int[n + 1];
        int result = 0;

        // 이미 계산된 결과(작은 문제)는 별도의 메모리 영역에 저장하여 다시 계산하지 않도록 한다.
        dp[1] = arr[1];

        // n이 1이 입력될 수도 있어서 조건을 추가한다.
        if (n >= 2) {
            dp[2] = arr[1] + arr[2];
        }

        // dp[i - 2]: 첫번째 계단
        // dp[i - 3] + arr[i - 1]: 두번째 계단
        // arr[i]: 현재 계단
        for (int i = 3; i <= n; i++) {
            dp[i] = Math.max(dp[i - 2], dp[i - 3] + arr[i - 1]) + arr[i];
        }

        System.out.println(dp[n]);

    }
}
```

## References

- [개발자로 취직하기 - 다이나믹 프로그래밍](https://www.youtube.com/watch?v=0bqfTzpWySY)
- [나동빈 - 다이나믹 프로그래밍](https://www.youtube.com/watch?v=5Lu34WIx2Us&t=131s)
