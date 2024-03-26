# 기본형과 참조형

자바의 변수 데이터 타입을 가장 크게 보면 기본형과 참조형으로 분류할 수 있다.

## 기본형

- 기본형(Primitive Type)은 `int`, `long`, `double`, `boolean` 처럼 변수에 사용할 값을 직접 넣을 수 있는 데이터 타입을 기본형(Primitive Type)이라 한다.
- 기본형은 선언과 동시에 크기가 정해진다. 따라서 크기를 동적으로 바꾸거나 할 수는 없다.
- 기본형은 더 빠르고 메모리를 효율적으로 처리한다. 다만 복잡한 데이터 구조를 만들고 관리할 수 없다.
- 기본형은 들어있는 값을 그대로 계산에 사용할 수 있다.

## 참조형

- 참조형(Reference Type)은 데이터에 접근하기 위한 참조(주소)를 저장하는 데이터 타입을 참조형(Reference Type)이라 한다.
- 참조형은 크기를 동적으로 할당할 수 있다. 이러한 것을 동적 메모리 할당이라 한다.
- 참조형은 더 복잡한 데이터 구조를 만들고 관리할 수 있다.
- 참조형은 들어있는 참조값을 그대로 사용할 수 없다. 주소지만 가지고는 할 수 있는게 없다. 주소지에 가야 실체가 있다.

### 기본형 대입

**자바는 항상 변수의 값을 복사해서 대입한다.**

```java
public class Main {
    public static void main(String[] args) {
        int tmp = 10;
        int sum = tmp;

        System.out.println("tmp = " + tmp); // 10
        System.out.println("Before sum = " + sum); // 10

        sum = 30;
        System.out.println("After tmp = " + tmp); // 10
        System.out.println("After sum = " + sum); // 30
    }

}
```

기본형은 값을 복사해서 대입한다. 따라서 `sum`의 값을 바꾼다고 해서 `tmp`의 값이 변경되지 않는다.

### 참조형 대입

```java
class Lecture {
    String name;
    int time;
}
public class Main {
    public static void main(String[] args) {
        Lecture l1 = new Lecture();
        Lecture l2 = l1;

        // study.javastudy.variable.Lecture@2ff4acd0
        System.out.println("l1 = " + l1);
        // study.javastudy.variable.Lecture@2ff4acd0
        System.out.println("l2 = " + l2);
    }

}
```

참조형의 경우 실제 사용하는 객체가 아니라 객체의 위치를 가리키는 참조값만 복사된다. 따라서 `l1`이 참조하고 있는 실제 값을 변경하면 `l2`가 참고하고 있는 실제 값도 같이 변경된다 (같은 참조를 하고 있기 때문). 서로 다른 참조를 하려면 각 인스턴스마다 `new` 키워드로 객체를 생성하면 된다.

## Reference

- [김영한의 실전 자바 - 기본편](https://www.inflearn.com/course/%EA%B9%80%EC%98%81%ED%95%9C%EC%9D%98-%EC%8B%A4%EC%A0%84-%EC%9E%90%EB%B0%94-%EA%B8%B0%EB%B3%B8%ED%8E%B8#)
