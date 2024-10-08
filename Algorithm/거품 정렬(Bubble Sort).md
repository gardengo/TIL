## 개요

__서로 인접한 두 원소의 대소를 비교하고, 조건에 맞지 않다면 자리를 교환하며 정렬하는 알고리즘__

## 프로세스 (오름차순)

1. 1번째 원소와 2번째 원소, 2번째 원소와 3번째 원소, ... , n-1번째 원소와 n번째 원소를 교환한다.
2. 1회전을 수행하면 가장 큰 원소가 맨 뒤로 이동. 이걸 n-1번 반복하면 정렬 완료.

![버블소트](src/bubble-sort-001.gif)

## Java Code (오름차순)

```java
void bubbleSort(int[] arr) {
    int size = arr.length;
    int tmp;
    for (int i = 1; i < size; i++) {
        for (int j = 0; j < size - i; j++) {
            if (arr[j] > arr[j + 1]) {
                tmp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = tmp;
            }
        }
    }
}
```

## 시간복잡도

`(n-1) + (n-2) + (n-3) + ... + 2 + 1 = n(n-1)/2`이므로 `O(n^2)`이다.

## 공간복잡도

주어진 배열 안에서 교환(swap)을 통해 정렬되므로 `O(n)`이다.

## 장점

- 구현이 매우 간단하고, 소스 코드가 직관적이다.
- 정렬하고자 하는 배열 안에서 교환하는 방식이므로 다른 메모리 공간을 필요로 하지 않는다. → 제자리 정렬(in-place sorting)
- 중복된 값을 순서대로 정렬하는 안정 정렬(Stable Sort)이다.

## 단점

- 시간복잡도가 최악, 최선, 평균 모두 `O(n^2)`으로 굉장히 비효율적이다.
- 정렬되어 있지 않은 원소가 정렬된 자리로 가기 위해서 교환 연산(swap)이 많이 일어난다.
