# 자바에서 가장 중요한 원칙

## 메서드에서 사용하는 용어 정리

### 메서드 호출

```java
호출: call("hello", 20)
메서드 정의: int call(String str, int age)
```

### 인수(Argument)

메서드를 호출할 때 `"hello"`, `20`처럼 넘기는 값을 영어로 Argument(아규먼트), 한글로 인수 또는 인자라 한다. 즉, Argument는 메서드 호출할 때 사용한다.

### 매개변수(Parameter)

메서드를 정의할 때 선언한 변수인 `String str`, `int age`를 매개변수, 파라미터라 한다.

## Call by Value와 Call by Referece

자바에서 정말 중요한 원칙이 있다.

- **자바는 항상 변수의 값을 복사해서 대입한다.**

### Call by Value

Call by Value는 메서드를 호출할 때 값을 넘겨주기 때문에 Pass by Value라고도 부른다. 메서드를 호출하는 호출자(Caller) 의 변수와 호출 당하는 수신자(Callee) 의 파라미터는 복사된 서로 다른 변수이다.

### Call by Reference

Call by Reference는 참조(주소)를 직접 전달하며 Pass By Reference라고도 부른니다. 참조를 직접 넘기기 때문에 호출자의 변수와 수신자의 파라미터는 완전히 동일한 변수이다. 따라서 메서드 내에서 파라미터를 수정하면 그대로 원본 변수에도 반영된다.

**자바는 오직 Call by Value로만 동작한다.**

**자바는 항상 변수의 값을 복사해서 대입한다.** 메서드 호출할 때 마찬가지로 매개변수(파라미터)도 결국 변수이기 때문에 값을 복사해서 넘긴다.

### 기본형 메서드 호출

```java
public class Main {
    public static void main(String[] args) {
        int a = 10;
        System.out.println("Before a = " + a); // 10
        changeInt(a);
        System.out.println("After a = " + a);
        // 20이 아닌 10 ?
    }

    public static void changeInt(int param) {
        param += 10;
    }
}
```

위와 같은 결과가 나오는 이유는 **메서드에서는 호출시점에 인자(Argument)를 읽고 복사해서 전달**하기 때문이다. 즉 변수 `param`의 값을 변경해도 변수 `a`의 값은 변하지 않는다.

### 참조형 메서드 호출

```java
class Lecture {
    String name;
    int time;

    @Override
    public String toString() {
        return "Lecture{" +
                "name='" + name + '\'' +
                ", time=" + time +
                '}';
    }
}
public class Main {
    public static void main(String[] args) {
        Lecture l1 = new Lecture();
        l1.name = "Math";
        l1.time = 30;
        System.out.println("Before li.toString() = " + l1.toString());
        // Before li.toString() = Lecture{name='Math', time=30}
        changeLecture(l1);
        System.out.println("After li.toString() = " + l1.toString());
        // After li.toString() = Lecture{name='English', time=50}
    }

    static void changeLecture(Lecture lecture) {
        lecture.name = "English";
        lecture.time = 50;
    }
}
```

기본형과 마찬가지로 메서드 호출시점에 인자(Argument)를 읽고 복사해서 전달한다. 여기서 인자는 참조값을 의미한다. 참조값을 복사해서 전달했기 때문에 `l1` 인스턴스와 메서드 파라미터의 `lecture` 인스턴스는 서로 같은 참조값을 가진다. (여기서 주의점은 참조값을 복사하는거지, **주소지 안의 실체 값까지 복사되는 것은 아니다.**)

## Reference

- [김영한의 실전 자바 - 기본편](https://www.inflearn.com/course/%EA%B9%80%EC%98%81%ED%95%9C%EC%9D%98-%EC%8B%A4%EC%A0%84-%EC%9E%90%EB%B0%94-%EA%B8%B0%EB%B3%B8%ED%8E%B8#)
- https://yaboong.github.io/java/2018/05/26/java-memory-management/
- https://bcp0109.tistory.com/360
