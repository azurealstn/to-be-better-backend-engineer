# 힙 정렬 (Heap Sort)

힙 정렬은 기본적으로 힙 자료구조를 사용한다. 따라서 [힙 자료구조](https://azurealstn.tistory.com/144)를 먼저 학습하면 좋다.

간단하게, 힙 자료구조는 최소값 또는 최대값을 빠르게 찾아내기 위해 완전 이진 트리 형태로 만들어진 자료구조이다. 그리고 힙 자료구조는 우선순위 큐(Priority Queue)를 구현하는데 기반이 된다.

## 힙 정렬 구현하기

- 가장 먼저 초기 상태의 배열을 별도의 배열 선언 없이 최대 힙(Max-Heap) 또는 최소 힙(Min-Heap)으로 만든다. 가장 작은 서브 트리부터 최대 힙을 만족하도록 순차적으로 진행하면 최대 힙을 만들 수 있다. (최소 힙도 마찬가지이며, 이와 같이 힙을 만드는 과정을 **heapify**라고 한다.) 최대 힙을 사용하면 오름차순으로, 최소 힙을 사용하면 내림차순으로 정렬된다.
- 힙에서 최대값(최소값)을 추출하고, 배열의 마지막 원소와 교환한다. 이 과정을 힙 추출(Heap Extraction)이라고 한다. 이렇게 추출된 원소는 정렬된 위치에 놓이게 된다.
- 힙 추출 후, 힙의 크기를 줄이고, 힙의 루트 노드를 다시 최대값(최소값)으로 만들어 준다. 이 과정을 힙 복원(Heap Restoration)이라고 한다.
- 위 과정을 힙의 크기가 1 이하가 될 때까지 반복한다. 과정을 완료하면 배열이 완전히 정렬된 상태가 된다.

### 코드보기

```java
import java.util.Arrays;

class HeapSort {

    // 힙 정렬 시작
    public void heapSort(int[] arr) {
        heapSort(arr, arr.length);
    }

    private void heapSort(int[] arr, int size) {

        /**
         * 부모노드와 heaify과정에서 음수가 발생하면 잘못 된 참조가 발생하기 때문에
         * 원소가 1개이거나 0개일 경우는 정렬 할 필요가 없으므로 바로 함수를 종료한다.
         */
        if (size < 2) {
            return;
        }

        /**
         * left child node = index * 2 + 1
         * right child node = index * 2 + 2
         * parent node = (index - 1) / 2
         */

        // 가장 마지막 요소의 부모 인덱스
        int parentIndex = getParent(size - 1);

        // Max Heap
        for (int i = parentIndex; i >= 0; i--) {
            heapify(arr, i, size - 1);
        }

        for (int i = size - 1; i > 0; i--) {
            /**
             *  root인 0번째 인덱스와 i번째 인덱스의 값을 교환해준 뒤
             *  0 ~ (i-1) 까지의 부분트리에 대해 max heap을 만족하도록 재구성한다.
             */
            swap(arr, 0, i);
            heapify(arr, 0, i - 1);
        }
    }

    // 부모 인덱스를 얻는 함수
    private static int getParent(int child) {
        return (child - 1) / 2;
    }

    // 두 원소를 교환하는 함수
    private void swap(int[] arr, int i, int j) {
        int tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    }

    // 힙을 재구성 하는 함수
    private void heapify(int[] arr, int parentIndex, int lastIndex) {
        /**
         * 현재 트리에서 부모 노드의 자식노드 인덱스를 각각 구해준다.
         * 현재 부모 인덱스를 가장 큰 값을 갖고있다고 가정한다.
         */
        int leftChildIndex = 2 * parentIndex + 1;
        int rightChildIndex = 2 * parentIndex + 2;
        int largestIndex = parentIndex;

        /**
         * 자식노드 인덱스가 트리의 크기를 넘어가지 않으면서
         * 왼쪽 자식이 largestIndex보다 크면 왼쪽 자식을 largestIndex로 설정
         */
        if (leftChildIndex <= lastIndex && arr[leftChildIndex] > arr[largestIndex]) {
            largestIndex = leftChildIndex;
        }

        /**
         * 자식노드 인덱스가 트리의 크기를 넘어가지 않으면서
         * 오른쪽 자식이 largestIndex보다 크면 오른쪽 자식을 largestIndex로 설정
         */
        if (rightChildIndex <= lastIndex && arr[rightChildIndex] > arr[largestIndex]) {
            largestIndex = rightChildIndex;
        }

        /**
         * largestIndex 와 부모노드가 같지 않다는 것은
         * 위 자식노드 비교 과정에서 현재 부모노드보다 큰 노드가 존재한다는 뜻이다.
         * 그럴 경우 해당 자식 노드와 부모노드를 교환해주고,
         * 교환 된 자식노드를 부모노드로 삼은 서브트리를 검사하도록 재귀 호출 한다.
         */
        if (largestIndex != parentIndex) {
            swap(arr, largestIndex, parentIndex);
            heapify(arr, largestIndex, lastIndex);
        }
    }
}
public class Record {
    public static void main(String[] args) {
        int[] arr = {8, 5, 22, 11, 2};

        HeapSort hs = new HeapSort();
        hs.heapSort(arr);

        System.out.println(Arrays.toString(arr));
    }
}
```

### 힙 정렬 특징

- 안정적이지 않은 정렬(Unstable Sort): 같은 값의 원소들이 정렬 과정에서 상대적인 순서가 변경될 수 있다.
- 제자리 정렬(In-place Sort): 입력 배열 안에서 정렬이 이루어지며, 추가적인 메모리를 사용하지 않는다.
- 시간 복잡도(Time Complexity): 최선, 평균, 최악의 경우 모두 `O(N logN)`을 갖는다.
- 외부 정렬(External Sorting): 힙 정렬은 외부 정렬에 적합한 알고리즘이다. 외부 정렬은 디스크와 같은 외부 저장소에 저장된 데이터를 정렬하는 과정에서 사용되며, 힙 정렬은 이 과정에서 효율적으로 사용될 수 있다.

### 힙 정렬 장점

- 시간복잡도가 최악의 경우에도 `O(N logN)`을 유지한다.
- 힙의 특징상 부분 정렬을 할 때 효과가 좋다.
- 메모리 사용량이 적다.

### 힙 정렬 단점

- 일반적인 `O(N logN)` 정렬 알고리즘에 비해 성능은 약간 떨어진다.
- 특징에서 보았듯이 안정적이지 않은 정렬이다. 따라서 안정성이 요구되는 경우에는 다른 알고리즘을 사용하는 것이 좋다.

<br>
<br>
<br>

## References

- https://st-lab.tistory.com/225
- https://moneylogging.tistory.com/entry/%EC%9E%90%EB%B0%94-%ED%9E%99%EC%A0%95%EB%A0%AC
