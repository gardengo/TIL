## 개요

__2번째 원소부터 시작하여 그 앞의 원소들과 비교하며 뒤로 옮기고 지정된 자리에 삽입하는 알고리즘__

## 프로세스 (오름차순)

1. 2번째 위치의 값을 저장한다.
2. 이전의 원소들과 비교하여 더 큰 경우 오른쪽으로 한 칸 이동시킨다.
3. 더 이상 큰 원소가 없을 때, 해당 위치에 저장했던 값을 삽입한다.
4. 다음 위치의 값을 저장하고 위 과정을 반복한다.

![삽입 정렬](src/insertion-sort-001.gif)

## Java Code (오름차순)

```java
void insertSort(int[] arr) {
    for (int index = 1; index < arr.length; index++) {
        int tmp = arr[index];
        int prev = index - 1;
        while (prev >= 0 && arr[prev] > tmp) {
            arr[prev + 1] = arr[prev];
            prev--;
        }
        arr[prev + 1] = tmp;
    }
}
```

## 시간복잡도

최악의 경우 `(n-1) + (n-2) + ... + 2 + 1 = n(n-1)/2`이므로 `O(n^2)`이다.<br>
최선의 경우 한 번씩만 비교하므로 `O(n)`이다.

## 공간복잡도

주어진 배열 안에서 교환(swap)을 통해 정렬되므로 `O(n)`이다.

## 장점

- 알고리즘이 단순하다.
- 대부분의 원소가 이미 정렬되어 있는 경우, 매우 효율적이다.
- 정렬하고자 하는 배열 안에서 교환하는 방식이므로 다른 메모리 공간을 필요로 하지 않는다. → 제자리 정렬(in-place sorting)
- 안정 정렬(Stable Sort)이다.
- Selection Sort나 Bubble Sort와 같은 `O(n^2)` 알고리즘에 비해 상대적으로 빠르다.

## 단점

- 평균과 최악의 시간복잡도가 `O(n^2)`으로 비효율적이다.
