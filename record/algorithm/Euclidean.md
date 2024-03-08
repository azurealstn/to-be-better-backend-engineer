# 유클리드 호제법

유클리드 호제법(유클리드 알고리즘)은 최대공약수를 구하는 알고리즘이다. 호제법이란 말은 두 수가 서로 상대방 수를 나누어서 결국 원하는 수를 얻는 알고리즘을 나타낸다.

2개의 자연수 a, b에 대해서 a를 b로 나눈 나머지를 r이라 하면(단, a>b), a와 b의 최대공약수는 b와 r의 최대공약수와 같다. 이 성질에 따라, b를 r로 나눈 나머지 r'를 구하고, 다시 r을 r'로 나눈 나머지를 구하는 과정을 반복하여 나머지가 0이 되었을 때 나누는 수가 a와 b의 최대공약수이다.

즉, a와 b의 최대공약수를 (a, b)로 나타낼 때,  
(a, b) = (b, r) 이 성립딘다.

## 예제

[프로그래머스 - 최대공약수와 최소공배수](https://school.programmers.co.kr/learn/courses/30/lessons/12940)

```java
import java.util.*;
import java.io.*;

public class 최대공약수와_최소공배수 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());
        System.out.println(Arrays.toString(solution(n, m)));
    }

    private static int[] solution(int n, int m) {
        int[] answer = new int[2];
        answer[0] = gcd(n, m);
        answer[1] = lcm(n, m);

        return answer;
    }

    // 최대공약수 구하기 (유클리드 호제법 이용)
    private static int gcd(int n, int m) {
        int a = Math.max(n, m);
        int b = Math.min(n, m);
        while (b != 0) {
            int r = a % b;
            a = b;
            b = r;
        }
        return a;
    }

    // 최소공배수 구하기
    // 최소공배수 * 최대공약수 = n * m 임을 이용
    // 따라서 최소공배수 = n * m / 최대공약수
    private static int lcm(int n, int m) {
        return n * m / gcd(n, m);
    }

}
```

## References

- https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95
- https://jisunshine.tistory.com/134
