# 변수 초기화

자바에서 변수는 반드시 초기화를 해야 한다. 안그러면 컴파일 에러를 발생시킨다.

```java
public class VariableInit {
    public static void main(String[] args) {
        int sum;
        System.out.println("sum = " + sum);
    }
}
```

- Error Message: `Variable 'sum' might not have been initialized`

자바는 왜 변수를 반드시 초기화를 해야 할까? 컴퓨터에서 메모리는 여러 시스템이 함께 사용하는 공간이다. 그래서 어떠한 값들이 계속 저장된다. 변소를 선언하면 메모리상의 어떤 공간을 차지하고 사용한다.

그런데 그 공간에 기존에 어떤 값이 있었는지는 아무도 모른다. 따라서 초기화를 하지 않으면 이상한 값이 출력될 수 있다. 이러한 문제를 예방하기 위해 자바는 변수를 초기화 하도록 강제한다.

위 예제에서 사용한 변수 `sum`은 지역 변수(Local Variable)인데, 지역 변수는 직접 초기화를 해주어야 한다. 하지만 클래스 변수와 인스턴스 변수는 자바가 자동으로 초기화를 진행한다.

```java
class Data {
    public int data;
}
public class VariableInit {
    public static int var; // 컴파일 에러가 발생하지 않는다!
    public static void main(String[] args) {
        System.out.println("var = " + var);

        Data data = new Data();
        System.out.println("data = " + data); // 자동으로 초기화 해준다.
    }
}
```

결과

```java
var = 0
data = study.javastudy.variable.Data@13221655
```

- 클래스 변수인 `int`형 var는 0으로 초기화 되었다.
- 인스턴스 변수인 data는 참조값으로 초기화 되었다.

## Reference

- [김영한의 자바 입문 - 코드로 시작하는 자바 첫걸음](https://www.inflearn.com/course/%EA%B9%80%EC%98%81%ED%95%9C%EC%9D%98-%EC%9E%90%EB%B0%94-%EC%9E%85%EB%AC%B8#)
