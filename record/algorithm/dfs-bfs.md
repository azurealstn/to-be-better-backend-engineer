> DFS와 BFS에 대한 개념 및 구현은 [링크](https://azurealstn.tistory.com/145)로 들어가서 확인할 수 있다.  
> 경로를 탐색할 때는 DFS, 그래프의 최단 거리를 구할 때는 BFS 알고리즘을 사용한다.

이번에는 DFS를 이용하여 아래 부분들을 구현해볼 것이다.

- 중복순열 구하기
- 순열 구하기
- 조합수(메모이제이션)
- 조합 구하기

#### 중복순열 구하기

1부터 N까지의 숫자중에서 중복을 허락하여 M번을 뽑아 나열한다.

```java
/**
 * 입력: 3 2
 * 중복순열은 dfs 메서드 안에 n만큼의 루프를 돌린다.
 */
public class Main {
    static int[] pm;
    static int n, m;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        pm = new int[m]; // 출력할 순열 배열

        dfs(0);
    }

    private static void dfs(int L) {
        if (L == m) {
            for (int x : pm) {
                System.out.print(x + " ");
            }
            System.out.println();
        } else {
            for (int i = 1; i <= n; i++) {
                pm[L] = i;
                dfs(L + 1);
            }
        }
    }
}
```

**결과**

```java
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

#### 순열 구하기

1부터 N까지의 숫자중에서 M번을 뽑아 나열한다. (중복은 허락하지 않는다.)

```java
/**
 * 입력: 3 2
 * 순열은 dfs 메서드 안에 n만큼의 루프를 돌린다.
 * 중복순열과 다르게 중복 허용이 안되므로 체크 배열이 있어야 한다.
 */
public class Main {
    static int[] pm, ch;
    static int n, m;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        pm = new int[m]; // 출력할 순열 배열
        ch = new int[n + 1]; // 중복을 제거할 체크 배열

        dfs(0);
    }

    private static void dfs(int L) {
        if (L == m) {
            for (int x : pm) {
                System.out.print(x + " ");
            }
            System.out.println();
        } else {
            for (int i = 1; i <= n; i++) {
                if (ch[i] == 0) {
                    ch[i] = 1; // 체크를 걸어준다.
                    pm[L] = i;
                    dfs(L + 1);
                    ch[i] = 0; // 백(Back) 할 때는 체크를 다시 풀어준다.
                }
            }
        }
    }
}
```

**결과**

```java
1 2
1 3
2 1
2 3
3 1
3 2
```

#### 조합수(메모이제이션)

수학에서 조합을 `Combination` 이다. 조합수를 구하는 공식이 있다. 여기서는 아래 공식을 숙지하면 문제를 풀 수 있다.

- `nCr` = `n-1Cr-1` + `n-1Cr`
- `nCr` -> `n == r` 혹은 `r == 0`이면 `nCr`의 값은 `1`이 된다.

재귀를 이용하여 조합수를 구하라.

```java
/**
 * 입력: 3 2
 * 메모이제이션을 활용하면 빠른 시간에 조합수를 구할 수 있다.
 */
public class Main {
    static int[][] dy; // 메모이제이션 2차원 배열
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int r = Integer.parseInt(st.nextToken());
        dy = new int[n + 1][n + 1];
        System.out.println(dfs(n, r));
    }

    private static int dfs(int n, int r) {
        if (dy[n][r] > 0) return dy[n][r];
        if (n == r || r == 0) return dy[n][r] = 1;
        return dy[n][r] = dfs(n - 1, r - 1) + dfs(n - 1, r);
    }
}
```

**결과**

```java
3
```

#### 조합 구하기

1부터 N까지의 숫자중에서 M개 뽑는 방법의 수를 출력한다.

```java
/**
 * 입력: 6 4
 * 시작 인덱스를 나타내는 s 변수가 필요하다.
 */
public class Main {
    static int[] combi;
    static int n, m;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = null;
        st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        combi = new int[m];
        dfs(0, 1); // 1부터 시작
    }

    private static void dfs(int L, int s) {
        if (L == m) {
            for (int x : combi) {
                System.out.print(x + " ");
            }
            System.out.println();
        } else {
            for (int i = s; i <= n; i++) {
                combi[L] = i;
                dfs(L + 1, i + 1);
            }
        }
    }
}
```

**결과**

```java
1 2 3 4
1 2 3 5
1 2 3 6
1 2 4 5
1 2 4 6
1 2 5 6
1 3 4 5
1 3 4 6
1 3 5 6
1 4 5 6
2 3 4 5
2 3 4 6
2 3 5 6
2 4 5 6
3 4 5 6
```

## References

- [자바(Java) 알고리즘 문제풀이 입문: 코딩테스트 대비](https://www.inflearn.com/course/%EC%9E%90%EB%B0%94-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%ED%85%8C%EB%8C%80%EB%B9%84#)
