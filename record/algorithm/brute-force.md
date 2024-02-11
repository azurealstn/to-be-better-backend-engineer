# 브루트 포스 (Brute Force)

## 브루트 포스 알고리즘

브루트 포스 알고리즘은 가능한 모든 경우의 수를 모두 탐색하면서 요구조건에 충족되는 결과만을 가져온다. 이 알고리즘의 강력한 점은 예외 없이 100%의 확률로 정답만을 출력한다. 그래서 브루트 포스 알고리즘을 완전 탐색 알고리즘이라고도 한다.

> 브루트 포스 (Brute Force)
>
> - Brute: 단순히
> - Force: 힘
>
> 단순히 힘만 갖고 밀어붙인다. 이는 머리는 쓰지 않고 모든 것을 다해보겠다는 의미로 브루트 포스 용어를 사용하였다.

브루트 포스는 주로 비밀번호 해킹할 때 사용했던 용어로, 자주 사용되는 비밀번호, 생년월일, 기념일 등으로 유추하여 해킹하는 것이 아닌 비밀번호가 조건에 맞을 수 있는 모든 조합을 다~ 시도해보는 기법을 `Brute Force Attack` 이라고 부른다.

### 브루트 포스 알고리즘 해결

- 일반적인 방법으로 문제를 해결하기 위해서는 모든 자료를 탐색해야 하기 때문에 **특정한 구조를 전체적으로 탐색할 수 있는 방법을 필요로** 한다.
- 알고리즘 설계의 가장 기본적인 접근 방법은 정답이 존재할 것으로 예상되는 모든 영역을 전체 탐색하는 방법이다.
- 선형 구조를 전체적으로 탐색하는 순차 탐색, 비선형 구조를 전체적으로 탐색하는 깊이 우선 탐색과 너비 우선 탐색이 가장 기본적인 도구이다.
  - 너비 우선 탐색은 브루트 포스와 관련이 깊다.

### 브루트 포스 알고리즘 구현

- `for/while`문 사용
- `recursion` 사용

브루트 포스 알고리즘을 사용하는 예제는 백준의 2798번: 블랙잭 문제가 있다. 이 문제 역시 전체 카드에서 3개를 고를 수 있는 경우의 수를 모두 탐색하여 각 경우별 선택한 카드들의 합을 모두 구한 뒤, 주어진 M을 넘지 않는 최대값을 찾는다. 여기서는 `3중 for문`을 사용하여 해결한다.

#### 코드보기

```java
import java.util.*;
import java.io.*;

public class Ex01 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());
        int[] arr = new int[n];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        int result = 0;

        //3중 for문으로 모든 경우의 수를 탐색한다.
        for (int i = 0; i < n - 2; i++) {
            for (int j = i + 1; j < n - 1; j++) {
                for (int k = j + 1; k < n; k++) {
                    int sum = arr[i] + arr[j] + arr[k];
                    if (sum == m) {
                        System.out.println(sum);
                        return;
                    }

                    result = Math.max(result, sum < m ? sum : result);
                }
            }
        }
        System.out.println(result);
    }
}
```

- 문제에 대한 자세한 풀이는 https://st-lab.tistory.com/97 참고

## References

- [개발자로 취직하기 - 브루트포스](https://www.youtube.com/watch?v=ZNa9-86uVEA&t=13s)
- https://hcr3066.tistory.com/26
