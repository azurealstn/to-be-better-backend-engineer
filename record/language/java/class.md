# 클래스

자바 세상은 클래스와 객체로 이루어져 있다. 그만큼 클래스와 객체라는 개념은 중요하다.

```java
public class Person {
    String name;
    int age;
}
```

**클래스에 정의한 변수들을 멤버 변수, 또는 필드**라 한다.

- **멤버 변수(Member Variable):** 이 변수들은 특정 클래스에 소속된 멤버이기 때문에 이렇게 부른다.
- **필드(Field):** 데이터 항목을 가리키는 전통적인 용어이다. 데이터베이스, 엑셀 등에서 데이터 각각의 항목을 필드라 한다.
- 자바에서 멤버 변수, 필드는 같은 뜻이다. 클래스에 소속된 변수를 뜻한다.

### 클래스, 객체, 인스턴스

클래스는 설계도이고, 이 설계도를 기반으로 실제 메모리에 만들어진 실체를 객체 또는 인스턴스라 한다. 둘다 같은 의미로 사용된다.

### 객체 생성

```java
public class Person {
    String name;
    int age;

    public static void main(String[] args) {
        Person person = new Person();
        System.out.println("person = " + person); // 참조값: study.javastudy.variable.Person@279f2327
        System.out.println(System.identityHashCode(person)); // 664740647
    }
}
```

- 객체를 사용하려면 먼저 설계도인 클래스를 기반으로 객체(인스턴스)를 생성해야 한다.
- 변수 person의 값은 객체의 메모리 주소번지를 나타낸다.
  - `System.identityHashCode(person)`을 사용하면 객체의 고유한 HashCode를 받을 수 있다. 해당 HashCode 값은 10진수로 출력된다.
  - 변수 person의 값에서 `@279f2327`, `@` 뒤에 나오는 `279f2327` 값은 HashCode로 출력한 10진수 값을 16진수로 변환한 값으로 출력된다. 이를 통해 변수 person의 값은 객체의 메모리 주소번지를 나타낸다는 것을 확인할 수 있다.
- 객체의 메모리 주소번지를 나타내는 변수 person을 통해 메모리에 있는 실제 객체를 접근하고 사용할 수 있다.

> 변수 person의 값에서 @앞은 패키지 + 클래스 정보를 뜻한다. @뒤에 16진수는 참조값을 뜻한다.

## 생성자

각 클래스마다 기본 생성자가 있다. 기본 생성자는 생략이 가능하다.

### 생성자가 필요한 이유

프로그래밍을 하다보면 객체를 생성하고 이후에 바로 초기값을 할당해야 하는 경우가 많다. 객체를 생성하는 시점에 어떤 작업을 하고 싶다면 생성자(Constructor)를 이용하면 된다.

```java
class Lecture {
    String name;
    int time;

    // 직접 정의한 생성자
    public Lecture(String name, int time) {
        this.name = name;
        this.time = time;
    }
}
public class Main {
    public static void main(String[] args) {
//        Lecture l1 = new Lecture(); // 컴파일 에러 발생!
        Lecture l1 = new Lecture("Math", 30);

    }
}
```

코드를 보면 직접 정의한 생성자가 있으면 자바가 기본 생성자를 자동으로 생성해주지 않는다. 따라서 `Lecture l1 = new Lecture();` 코드는 컴파일 에러가 발생한다. 즉, 직접 정의한 생성자를 통해 필수값 입력을 보장할 수 있다.

## Reference

- [김영한의 실전 자바 - 기본편](https://www.inflearn.com/course/%EA%B9%80%EC%98%81%ED%95%9C%EC%9D%98-%EC%8B%A4%EC%A0%84-%EC%9E%90%EB%B0%94-%EA%B8%B0%EB%B3%B8%ED%8E%B8#)
