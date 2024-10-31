## 개요

**힙 정렬(Heap Sort)** 은 완전 이진 트리의 일종인 힙(Heap) 자료구조를 기반으로 하는 정렬 알고리즘이다. 최대 힙(Max Heap)을 구성하여 정렬하는 방법으로, 내림차순으로 정렬하고자 할 때는
최소 힙(Min Heap)을 구성하여 정렬한다.

## 프로세스 (오름차순)

1. 주어진 배열을 최대 힙으로 구성한다(Heapify).
2. 힙의 루트(최댓값)를 마지막 요소와 교환하고 힙의 크기를 1 감소시킨다.
3. 루트 노드에 대해 다시 힙 속성을 만족하도록 재구성한다.
4. 힙의 크기가 1이 될 때까지 2-3 과정을 반복한다.

![힙 소트](src/Heap_sort_example.gif)

## Array Code (오름차순)

```java
public class HeapSort {
    public void heapSort(int[] arr) {
        int n = arr.length;

        // 초기 힙 구성
        for (int i = n / 2 - 1; i >= 0; i--)
            heapify(arr, n, i);

        // 힙에서 요소를 하나씩 추출
        for (int i = n - 1; i > 0; i--) {
            // 루트를 마지막 요소와 교환
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;

            // 줄어든 힙에 대해 heapify 수행
            heapify(arr, i, 0);
        }
    }

    // 힙을 재구성하는 함수
    private void heapify(int[] arr, int n, int i) {
        int largest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;

        // 왼쪽 자식이 더 큰 경우
        if (left < n && arr[left] > arr[largest])
            largest = left;

        // 오른쪽 자식이 더 큰 경우
        if (right < n && arr[right] > arr[largest])
            largest = right;

        // largest가 변경된 경우 교환
        if (largest != i) {
            int swap = arr[i];
            arr[i] = arr[largest];
            arr[largest] = swap;

            // 재귀적으로 영향받은 하위 트리 재구성
            heapify(arr, n, largest);
        }
    }
}
```

## 시간복잡도

**최선의 경우(Best cases):** `O(nlog₂n)`

- 초기 힙 구성: `O(n)`
- n개의 요소에 대해 힙 재구성: `O(log₂n)`
- 전체 시간 복잡도: `O(nlog₂n)`

**최악의 경우(Worst cases):** `O(nlog₂n)`

- 초기 힙 구성: `O(n)`
- n개의 요소에 대해 힙 재구성: `O(log₂n)`
- 전체 시간 복잡도: `O(nlog₂n)`

**평균의 경우(Average cases):** `O(nlog₂n)`

## 공간복잡도

- 원본 배열: `O(n)`
- 추가 공간: `O(1)` (제자리 정렬)
- 총 공간복잡도: `O(n)`

## 장점

- 추가 메모리를 거의 필요로 하지 않는 제자리 정렬이다.
- 최선, 평균, 최악의 경우 모두 `O(nlog₂n)`으로 안정적인 성능을 보장한다.
- 우선순위 큐를 구현하는데 유용하다.
- 가장 크거나 작은 k개의 요소를 찾을 때 유용하다.

## 단점

- 불안정 정렬(Unstable Sort)이다.
- 데이터의 상태에 따라 퀵 정렬보다 성능이 떨어질 수 있다.
- 이미 정렬된 데이터에 대해서도 `O(nlog₂n)`의 시간이 소요된다.
- 재귀적 구조로 인한 성능 저하가 발생할 수 있다.