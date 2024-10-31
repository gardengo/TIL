## 개요

**기수 정렬(Radix Sort)** 은 비교 연산을 하지 않고 정렬하는 알고리즘으로, 데이터의 각 자릿수를 순서대로 비교하여 정렬하는 방식이다. 각 자릿수별로 버킷(데이터를 담을 수 있는 공간)을 만들어
분류하고, 다시 순서대로 가져와서 정렬하는 방식을 반복한다.

## 프로세스 (오름차순)

1. 데이터의 최대 자릿수를 파악한다.
2. 가장 낮은 자릿수부터 시작하여 각 자릿수별로:
    - 0~9까지의 버킷을 준비한다.
    - 현재 자릿수를 기준으로 버킷에 데이터를 분류한다.
    - 버킷에서 순서대로 데이터를 다시 가져온다.
3. 가장 높은 자릿수까지 2번 과정을 반복한다.

![기수 정렬](src/radix-sort.gif)

## Java Code (오름차순)

```java
public class RadixSort {
    public void radixSort(int[] arr) {
        // 배열에서 최댓값 찾기
        int max = getMax(arr);

        // 각 자릿수별로 계수 정렬 수행
        for (int exp = 1; max / exp > 0; exp *= 10)
            countSort(arr, exp);
    }

    private int getMax(int[] arr) {
        int max = arr[0];
        for (int i = 1; i < arr.length; i++)
            if (arr[i] > max)
                max = arr[i];
        return max;
    }

    private void countSort(int[] arr, int exp) {
        int n = arr.length;
        int[] output = new int[n];
        int[] count = new int[10];

        // 현재 자릿수를 기준으로 개수 세기
        for (int i = 0; i < n; i++)
            count[(arr[i] / exp) % 10]++;

        // count 배열 누적합 계산
        for (int i = 1; i < 10; i++)
            count[i] += count[i - 1];

        // 뒤에서부터 순회하며 output 배열 구성
        for (int i = n - 1; i >= 0; i--) {
            output[count[(arr[i] / exp) % 10] - 1] = arr[i];
            count[(arr[i] / exp) % 10]--;
        }

        // output 배열을 원본 배열로 복사
        for (int i = 0; i < n; i++)
            arr[i] = output[i];
    }
}
```

## 시간복잡도

**최선의 경우(Best cases):** `O(d(n+k))`

- d: 최대 자릿수
- n: 데이터의 개수
- k: 각 자릿수의 표현 범위 (일반적으로 10)

**최악의 경우(Worst cases):** `O(d(n+k))`

**평균의 경우(Average cases):** `O(d(n+k))`

## 공간복잡도

- 원본 배열: O(n)
- 임시 배열: O(n)
- 카운트 배열: O(k)
- 총 공간복잡도: O(n+k)

## 장점

- 비교 연산을 하지 않는 정렬 알고리즘이다.
- 자릿수가 고정되어 있을 때 매우 빠른 정렬 속도를 보인다.
- 안정 정렬(Stable Sort)이다.
- 정수나 문자열 등 자릿수가 있는 데이터에 대해 효과적이다.

## 단점

- 데이터 전체의 크기에 기수(radix)의 크기만한 메모리가 더 필요하다.
- 자릿수가 없는 데이터에는 적용할 수 없다.
- 자릿수가 많은 경우 비효율적일 수 있다.
- 음수를 정렬할 때는 추가적인 처리가 필요하다.
- 데이터의 길이가 다른 경우에는 추가적인 처리가 필요하다.
