# 배열(Array)과 리스트(List)

## 목차

- [배열(Array)](#배열array)
- [리스트(List)](#리스트list)
- [ArrayList](#arraylist)
- [LinkedList](#linkedlist)

## 배열(Array)

- 같은 타입의 데이터들을 저장하는 자료구조
- 연속된 메모리 공간에 데이터들을 저장
- 데이터들 각각은 이름이 없지만 인덱스로 접근 가능

### 배열의 장점

- 구현이 쉽다.
- 인덱스를 이용한 무작위 접근(random access)이 가능하므로 검색 성능이 좋다.
- 순차 접근(sequential access)의 경우에도 배열을 데이터를 하나의 연속된 메모리 공간에 할당하므로 연결리스트(Linked list)보다 빠르다.
- 참조를 위한 추가적인 메모리 할당이 필요없다.

### 배열의 단점

- 자료의 삽입과 삭제에 비효율적이다. 데이터를 하나의 연속된 메모리 공간에 할당하기 때문에 배열 중간에 Insert, Delete시 다음 항목의 모든 요소를 이동시켜야 한다. (Shift 연산 작업)
- 배열은 생성 후 지정한 크기를 바꿀 수 없기 때문에(고정된 크기) 너무 크게 잡으면 메모리가 낭비되고, 너무 작게 잡으면 그 이상의 자료를 저장할 수 없게 된다.
- 메모리의 낭비가 발생한다. 배열은 초기 사이즈만큼의 메모리를 할당 받아 사용하기 때문에 데이터 존재 유무와 상관없이 일정한 크기의 메모리 공간을 점유하고 있다. 즉, 이미 삭제한 데이터라도 배열 자체를 메모리에서 제거되지 않는 이상 데이터의 메모리 공간을 재사용할 수 없다.

## 리스트(List)

- 값(value)들을 저장하는 추상자료형(ADT)
- 순서가 있음
- 중복을 허용

### ADT: 추상자료형(Abstract Data Type)

순수하게 기능이 무엇인지 나열한 것을 가리켜 추상자료형(ADT)라고 한다. 특정 자료형과 그 자료형을 바탕으로 하는 기능들(함수들)의 집합을 ADT라고 한다.

연결리스트 insert, delete 등과 같은 기능들(함수)과 함께 작동하는 자료구조이다. 스택 역시 push, pop, peek, empty 등과 같은 기능들과 같이 정의되어야 비로소 작동하게 된다.

그렇기에 자료구조(연결리스트, 스택, 큐 등)의 ADT는 데이터를 담을 저장소를 만드는 것과 데이터를 다루는 함수들을 정의하는 것을 포함하는 개념인 것이다. 즉, 자료구조의 특징뿐만 아니라 해당 자료구조를 어떻게(How) 사용하는지까지 내포되어 있는 것이 바로 ADT이다.

### 리스트의 장점

- 자료의 삽입과 삭제에 효율적이다. 데이터를 불연속적으로 메모리 공간에 할당하고 있고, 포인터를 통하여 다음 데이터의 위치를 가르키고 있어 삽입 삭제시 용이하다.
- 배열에 비해 고정된 크기가 아니라 동적 크기이므로 초기 사이즈를 고려하지 않아도 된다.
- 메모리의 낭비가 발생하지 않는다. 포인터를 통하여 다음 데이터의 위치를 가르키고 있어서 빈틈없는 데이터 적재가 가능하다.

### 리스트의 단점

- 검색 성능이 좋지 않다. 포인터를 통하여 다음 데이터를 찾을 수 있기 때문에 처음부터 데이터를 찾아나가야 한다. 최악의 경우에는 모든 데이터를 검색할 수 밖에 없다.
- 참조를 위한 추가적인 메모리 할당이 필요하다.

## ArrayList

ArrayList에 대한 자세한 설명은 https://azurealstn.tistory.com/147 블로그 참고를 바란다.

Array와 ArrayList는 요소를 추가하거나 가져올 때의 성능은 비슷하다. 두 작업 모두 일정한 시간에 실행된다. ArrayList 역시 Array의 특징을 그대로 가지고 있다. Array의 가장 큰 단점 중 하나가 바로 고정된 크기라는 점이다. 이를 개선하기 위해 나온 것이 ArrayList이다.

ArrayList는 List와 같이 동적 크기를 갖는다. 이를 동적 배열(Dynamic Array)이라고도 한다. ArrayList는 동적 크기를 갖기 위해 resize를 수행한다. 요소를 추가하거나 가져올 때의 성능은 배열과 비슷하지만 resize를 수행할 때는 성능이 저하된다.

## LinkedList

LinkedList는 ArrayList와 같이 인덱스로 접근하여 조회 / 삽입이 가능하지만 내부 구조는 완전히 다르게 구성되어 있다. ArrayList는 내부적으로 배열을 이용하지만 LinkedList는 내부적으로 List를 이용하여 노드(객체)끼리의 주소 포인터를 서로 가리키며 링크(참조)함으로써 이어지는 구조이다.

LinkedList의 가장 큰 특징은 ArrayList와 다르게 중간에 데이터가 추가되거나 삭제되어도 데이터를 이동(Shift)시키지 않아도 된다는 점이다. 그 이유는 추가되거나 삭제될 노드의 위치의 앞뒤쪽에 노드의 참조를 변경하기만 하면 된다. 또한 LinkedList는 List의 특징을 가지고 있기 때문에 고정된 크기가 아닌 동적 크기를 가지고 있다.

## References

- [쉬운코드 - 자료구조 배열편](https://www.youtube.com/watch?v=Hpg6zS0Nq28&list=PLcXyemr8ZeoR82N8uZuG9xVrFIfdnLd72&index=3)
- [쉬운코드 - 자려구조 리스트편](https://www.youtube.com/watch?v=xvi-n11kym0&list=PLcXyemr8ZeoR82N8uZuG9xVrFIfdnLd72&index=5)
- https://codedragon.tistory.com/7468
- https://devlogofchris.tistory.com/42
- [velog - Array vs ArrayList](https://velog.io/@humblechoi/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-Array-vs-ArrayList)
- [Java - LinkedList 구조](https://inpa.tistory.com/entry/JAVA-%E2%98%95-LinkedList-%EA%B5%AC%EC%A1%B0-%EC%82%AC%EC%9A%A9%EB%B2%95-%EC%99%84%EB%B2%BD-%EC%A0%95%EB%B3%B5%ED%95%98%EA%B8%B0)
- [ADT란](https://m.blog.naver.com/demonic3540/221227400125)
