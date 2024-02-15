# 형변환

- 작은 범위에서 큰 범위로는 당연히 변환할 수 있다.
  - 예) int -> long -> double
- 큰 범위에서 작은 범위로는 문제가 발생할 수 있다.
  - 소수점 버림
  - 오버플로우

## 기본형 형변환

가장 먼저 쉬운 기본형(Primitive Type) 형변환에 대해 알아보자.

### 자동 형변환

```java
public class Main {
    public static void main(String[] args) {
        int value = 5;
        long bigValue = value;
//        long bigValue1 = (long) value; // (long) 생략 가능
        System.out.println("bigValue = " + bigValue); // 5
    }
}
```

작은 범위에서 큰 범위로 변환하는 것을 **자동 형변환 또는 묵시적 형변환** 이라 한다. 이러한 경우 자바에서는 자동으로 형변환을 시켜주어 `(long)` 생략이 가능하다.

### 명시적 형변환

```java
public class Main {
    public static void main(String[] args) {
        long bigValue = 5;
//        int value = bigValue; // 컴파일 에러 발생!
        int value = (int) bigValue;
        System.out.println("value = " + value); // 5
    }
}
```

큰 범위에서 작은 범위로 변환하는 것을 **명시적 형변환** 이라 한다. 명시적으로 `(int)`를 써야 한다. 어떻게 보면 명시적이 당연하다. 큰 범위에서 작은 범위로 변환할 경우 데이터 손실이 발생할 수 있고, 의도치 않은 결과를 불를 수 있는데 개발자가 이를 인지하고도 사용할 것인지 되려 물어보는 셈이다.

```java
public class Main {
    public static void main(String[] args) {
        long bigValue = Integer.MAX_VALUE;
        int value = (int) bigValue + 1;
        System.out.println("value = " + value); // -2147483648
    }
}
```

위 코드와 같이 int형의 최대 범위에서 `+1` 연산을 하면 전혀 다른 결과값이 나오는 것을 확인할 수 있다. 그래서 개발자는 명시적 형변환시 조심히 다루어야 한다.

## 참조형 형변환

- 업캐스팅(upcasting): 부모 타입으로 변경
- 다운캐스팅(downcasting): 자식 타입으로 변경

### 업캐스팅

```java
public class CastingMain3 {
    public static void main(String[] args) {
        Child child = new Child();
        Parent parent1 = (Parent) child; //업캐스팅은 생략 가능, 생략 권장
        Parent parent2 = child; //업캐스팅 생략

        parent1.parentMethod();
        parent2.parentMethod();
    }
}
```

원래라면 `Parent parent1 = (Parent) child;` 처럼 캐스팅 명시를 해줘야하지만 업캐스팅의 경우 생략이 가능하고, 권장한다.

```java
Parent parent2 = child
Parent parent2 = new Child()
```

업캐스팅은 생략할 수 있다. 다운캐스팅은 생략할 수 없다. 참고로 업캐스팅은 매우 자주 사용하기 때문에 생략을 권장한다. 자바에서 부모는 자식을 담을 수 있다. 하지만 그 반대는 안된다. (꼭 필요하다면 다운캐스팅을 해야 한다.)

### 다운캐스팅

다운캐스팅은 잘못하면 심각한 런타임 오류가 발생할 수 있다.

```java
public class CastingMain4 {
    public static void main(String[] args) {
        Parent parent1 = new Child(); // 다형성 참조
        Child child1 = (Child) parent1;
        child1.childMethod(); //문제없음

        Parent parent2 = new Parent();
        Child child2 = (Child) parent2; //런타임 오류 - ClassCastException
        child2.childMethod(); //실행 불가
    }
}
```

> 다형성 참조란, 부모 타입의 변수가 자식 인스턴스 참조하는 것을 말한다.

업캐스팅의 경우 이런 문제가 절대로 발생하지 않는다. 왜냐하면 객체를 생성하면 해당 타입의 상위 부모 타입은 모두 함께 생성된다. 업캐스팅은 메모리 상에 인스턴스가 모두 존재하기 때문에 항상 안전하다. 따라서 캐스팅을 생략할 수 있다.

반면에 다운캐스팅의 경우 인스턴스에 존재하지 않는 하위 타입으로 캐스팅하는 문제가 발생할 수 있다. 왜냐하면 객체를 생성하면 부모 타입은 모두 함께 생성되지만 자식 타입은 생성되지 않는다. 따라서 개발자가 이런 문제를 인지하고 사용해야 한다는 의미로 명시적으로 캐스팅을 해주어야 한다. 안전하게 디운캐스팅하려면 `instanceof` 키워드로 다운캐스팅하려는 자식 인스턴스를 참조하고 있는지 확인하여 다운캐스팅을 하면 된다.

### instanceof

다형성에서 참조형 변수는 이름 그대로 다양한 자식을 대상으로 참조할 수 있다. `instanceof` 키워드를 사용하면 어떤 인스턴스를 참조하고 있는지 확인할 수 있다.

```java
new Parent() instanceof Parent
Parent p = new Parent() //같은 타입 true

new Child() instanceof Parent
Parent p = new Child() //부모는 자식을 담을 수 있다. true

new Parent() instanceof Child
Child c = new Parent() //자식은 부모를 담을 수 없다. false

new Child() instanceof Child
Child c = new Child() //같은 타입 true
```

## Reference

- [김영한의 실전 자바 - 기본편](https://www.inflearn.com/course/%EA%B9%80%EC%98%81%ED%95%9C%EC%9D%98-%EC%8B%A4%EC%A0%84-%EC%9E%90%EB%B0%94-%EA%B8%B0%EB%B3%B8%ED%8E%B8#)
