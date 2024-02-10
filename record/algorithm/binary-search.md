# 이분 탐색

> [트리란?](https://azurealstn.tistory.com/143)  
> 트리와 이분 탐색에 대한 개념은 위 링크 참고

## 이분 탐색 개념

이진 탐색은 현재 노드를 기준으로 왼쪽 노드와 그 이하 노드들은 현재 노드보다 작아야 하고, 오른쪽 노드와 그 이하 노드들은 현재 노드보다 커야 한다.

![image](/record/algorithm/images/image.png)

- 위 그림은 7 노드를 기준으로 했지만 5, 8 노드도 동일하다.

## 이분 검색 알고리즘

이진 검색 알고리즘(Binary Search Algorithm)은 오름차순으로 정렬된 리스트에서 특정한 값의 위치를 찾는 알고리즘이다. 검색 원리상 **정렬된 리스트에만 사용**할 수 있다는 단점이 있지만, 검색이 반복될 때마다 목표값을 찾을 확률은 두 배가 되므로 **속도가 빠르다는 장점**이 있다.

이분 검색의 시간복잡도는 `O(log N)`이고, 처음부터 끝까지 탐색하는 완전 탐색보다는 훨씬 빠르다.

### 진행순서

- 우선 정렬
- 배열의 첫 번째 인덱스(startIndex)와 마지막 인덱스(endIndex) 선언
- startIndex와 endIndex가 서로 교차되기 전까지 루프를 돈다.
- 배열의 중간 인덱스(midIndex) 선언
- 찾으려는 수를 찾은 경우 `break`
- 찾으려는 수가 중간값보다 큰 경우 `endIndex = midIndex - 1`
- 찾으려는 수가 중간값보다 큰 경우 `startIndex = midIndex + 1`

### 코드구현

```java
import java.util.*;
import java.io.*;

public class Ex01 {
    public static void main(String[] args) throws IOException {
        /**
         * 입력값:
         *  - n: 배열의 개수
         *  - m: 찾으려는 수
         *  - arr: 배열
         * 출력값:
         *  - 정렬 후 찾으려는 수가 몇 번째에 있는지 출력
         */
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

        Arrays.sort(arr); // 가장 먼저 배열을 정렬시킨다.

        int startIndex = 0; // 배열의 첫 번째 인덱스
        int endIndex = arr.length - 1; // 배열의 마지막 인덱스
        int result = 0; // 출력값

        /**
         * startIndex와 endIndex가 서로 교차되기 전까지 반복
         * startIndex > endIndex 이 되는 순간 서로 교차된다.
         */
        while (startIndex <= endIndex) {
            int midIndex = (startIndex + endIndex) / 2; // 배열의 중간 인덱스
            if (arr[midIndex] == m) { // 찾으려는 수를 찾은 경우
                result = midIndex + 1;
                break;
            } else if (arr[midIndex] > m) { // 찾으려는 수가 중간값보다 큰 경우
                endIndex = midIndex - 1;
            } else { // 찾으려는 수가 중간값보다 큰 경우
                startIndex = midIndex + 1;
            }
        }

        System.out.println(result);
    }
}
```

## References

- https://ko.wikipedia.org/wiki/%EC%9D%B4%EC%A7%84_%EA%B2%80%EC%83%89_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Algorithm/Binary%20Search.md
