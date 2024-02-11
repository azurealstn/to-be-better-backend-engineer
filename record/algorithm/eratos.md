# 에라토스테네스의 체

수학에서 에라토스테네스의 체는 소수를 찾는 빠르고 쉬운 방법이다. 에라토스테네스의 체가 어떻게 알고리즘이 수행되는지 [그림](https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4)을 통해 확인할 수 있다.

> **소수**  
> 소수는 1보다 큰 자연수 중 1과 자기 자신만을 약수로 가지는 수다.  
> 약수는 어떤 수를 나누어 떨어지게 하는 수를 말한다.

## 에라토스테네스의 체 알고리즘

![eratos-1](/record/algorithm/images/eratos-1.png)

1. 기본적으로 자연수+1 만큼의 체크 배열(`ch`)을 만들어둔다. 소수가 아닌 숫자들을 걸러내기 위한 배열이다. (참고로 소수는 1보다 커야하므로 1은 제외한다.)
2. 이제 자연수만큼 루프를 돌려서 체크가 안된 경우 카운트 해준다. 그리고 해당 자연수(`2`)의 배수들은 모두 체크 배열에서 체크 처리해준다.
3. 다음 자연수 `3`은 체크가 안됐으므로 카운트 해주고, `3`의 배수들은 모두 체크 배열에서 체크 처리해준다.
4. 위 과정 반복 (이하 생략...)

### 코드보기

```java
/**
 * 입력:
 *  -> n: 자연수의 개수
 * 출력:
 *  -> 소수의 개수
 */
public class Ex01 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        int n = Integer.parseInt(br.readLine());
        int[] ch = new int[n + 1]; // 자연수+1 만큼의 체크 배열
        int cnt = 0; // 소수의 개수

        for (int i = 2; i <= n; i++) { // 자연수 2부터 반복
            if (ch[i] == 0) { // 체크가 안된 경우
                cnt++;
                for (int j = i; j <= n; j = j + i) { // i배수씩 증간한다.
                    ch[j] = 1; // 체크 처리
                }
            }
        }

        System.out.println(cnt); // 출력
    }
}
```

## References

- https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4
