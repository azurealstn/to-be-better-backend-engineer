# Two pointers, Sliding window

## Two Pointers 알고리즘

- 리스트에 순차적으로 접근해야 할 때 **두 개의 점의 위치를 기록하면서 처리**하는 알고리즘
- 정렬되어있는 두 리스트의 합집합에도 사용되기도 하고, 병합정렬의 Counquer 영역의 기초가 되기도 한다.
- 일반적으로 투 포인터를 사용하지 않고 문제를 풀면 2중 for문을 사용해야하기 때문에 `O(N^2)`이 걸린다. 하지만 투 포인터를 사용하면 `O(N)`으로 단축된다.
- 두 개의 포인터를 가지고 처리하기 때문에 알고리즘 자체는 어렵지 않다.

### Two Pointers 예제

백준 사이트의 [11728번: 배열합치기](https://www.acmicpc.net/problem/11728) 문제를 풀어보면 투 포인터 알고리즘이 무엇인지 금방 알 수 있다. 여기서는 단순히 코드를 통해 투 포인터가 대략 어떤건지 확인한다.

```java
import java.util.*;
import java.io.*;

/**
 * 투 포인터 알고리즘
 * O(N^2) -> O(N)
 */
public class Ex01 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());

        // 정렬되어 있는 두 배열
        int[] a = new int[n];
        int[] b = new int[m];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            a[i] = Integer.parseInt(st.nextToken());
        }
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < m; i++) {
            b[i] = Integer.parseInt(st.nextToken());
        }

        // 결과를 출력할 리스트
        ArrayList<Integer> list = new ArrayList<>();

        // 두 개의 포인터 선언
        int p1 = 0;
        int p2 = 0;

        // 배열의 어느 한 쪽이 끝에 도달할 때 까지 반복
        while (p1 < n && p2 < m) {
            // a와 b 배열중 작은 값을 먼저 리스트에 넣고,
            // 작은 값을 넣은 배열의 포인터를 하나 증가한다.
            if (a[p1] < b[p2]) list.add(a[p1++]);
            else list.add(b[p2++]);
        }

        // 배열의 어느 한 쪽이 끝에 도달한 경우
        // 아직 도달하지 못한 배열에서 나머지 작업을 수행한다.
        while (p1 < n) list.add(a[p1++]);
        while (p2 < m) list.add(b[p2++]);

        StringBuilder sb = new StringBuilder();
        for (int x : list) {
            sb.append(x).append(" ");
        }
        System.out.print(sb);
    }
}
```

## Sliding Window 알고리즘

- **고정 사이즈의 윈도우가 이동**하면서 윈도우 내에 있는 데이터를 이용해 문제를 풀이하는 알고리즘을 말한다.
- 교집합의 정보를 공유하고, 차이가 나는 양쪽 끝 원소만 갱신하는 방법이다.
- 배열이나 리스트의 요소의 일정 범위의 값을 비교할 때 사용하면 매우 유용하다.
- 투 포인터(two poitners) 알고리즘과 연동하여 많이 쓰인다.
- 1차원 배열이 있고 이 배열에서 각자 다른 원소를 가리키는 2개의 포인터를 조작하며 원하는 값을 얻는 형태
- 원래 네트워크에서 사용되던 알고리즘을 문제풀이에 응용한 경우라고 할 수 있다.

![two-pointers-1](/record/algorithm/images/two-pointers-1.png)
(출처: https://velog.io/@zwon/%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%94%A9-%EC%9C%88%EB%8F%84%EC%9A%B0Sliding-Window)

> 위 이미지를 보면 투 포인트 알고리즘은 구간의 넓이가 조건에 따라 유동적으로 변하며, 슬라이딩 윈도우 알고리즘은 항상 구간의 넓이가 고정되어 있다는 차이점이 있습니다.

### Sliding Window 예제

1, 2, 3, 4, 5, 6, 7 로 이루어진 숫자 배열에서 A[i] + A[i+1] + A[i+2] 형식으로 **연속적인 3개의 숫자**의 합의 최댓값을 구해라.

문제의 포인트(Tip)는 Sliding Window는 고정된 사이즈의 윈도우가 이동하는 것이기 때문에 **연속적인** 이라는 단어가 중요하다.

**연속적인 3개의 숫자**의 합의 최댓값을 구한다고 가정해보면 아래 5가지의 경우의 수가 나온다.

- [1, 2, 3], 4, 5, 6, 7
- 1, [2, 3, 4], 5, 6, 7
- 1, 2, [3, 4, 5], 6, 7
- 1, 2, 3, [4, 5, 6], 7
- 1, 2, 3, 4, [5, 6, 7]

1. 먼저 처음 배열 [1,2,3] 의 합을 구한다.
2. 다음 배열인 [2,3,4]는 [1,2,3] 배열에서 맨 앞의 값인 1을 뻬고, 그 다음 값인 4를 더한다.
3. 이러한 규칙으로 다음 배열의 값은 전 배열에서 처음 원소를 빼고 다음에 들어올 원소를 더해주면 된다는 것을 알 수 있다.

**간단하게 코드를 작성해보자.**

```java
import java.util.*;
import java.io.*;

public class Ex01 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        // 입력은 생략..
        int[] arr = {1, 2, 3, 4, 5, 6, 7}; // 배열
        int k = 3; // 연속적인 숫자를 더할 개수
        int answer = 0; // 출력할 변수
        int sum = 0; // 연속적인 숫자의 합

        // 먼저 처음 배열 [1,2,3] 의 합을 구한다.
        for (int i = 0; i < k; i++) {
            sum += arr[i];
        }
        answer = sum;

        // 다음 배열인 [2,3,4]는 [1,2,3] 배열에서 맨 앞의 값인 1을 뻬고, 그 다음 값인 4를 더한다.
        for (int i = k; i < arr.length; i++) {
            sum = sum - arr[i - k] + arr[i];
            // 최대값을 구한다.
            answer = Math.max(answer, sum);
        }

        System.out.println(answer);
    }
}
```

> 정리하면 투 포인터(Two Poitners) 알고리즘과 슬라이딩 윈도우(Sliding Window) 알고리즘 같이 사용하는 경우가 많고, 시간복잡도를 `O(N^2)`에서 `O(N)`으로 단축시킬 수 있다.

## References

- https://butter-shower.tistory.com/226
- https://ji-musclecode.tistory.com/37
