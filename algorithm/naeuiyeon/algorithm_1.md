# 1. 시간복잡도(Time Complexity)
- 알고리즘이 입력 크기에 따라 실행하는 연산의 수를 측정하는 지표로, 알고리즘의 효율성을 평가하는데 사용
- 주로 입력 크기(n)가 커질수록 알고리즘의 실행시간이 얼마나 빨리 증가하는 지를 나타내며, 빅-오 표기법(Big-O Notaiton)으로 표현
## 1.1. 시간복잡도 중요도
- 효율적인 알고리즘 설계
  - Time Complexity를 통해 Algorithm의 성능을 비교하고, 더 나은 Algorithm을 선택 가능
- 대규모 데이터 처리
  - Time Complexity가 높은 Algorithm은 큰 입력을 처리할 때 실행 시간이 크게 증가하여 성능이 저하될 수 있음
- 성능 예측
  - 최적화할 부분을 식별하고, 더 효율적인 코드 개선 가능
## 1.2. 빅-오 표기법(Big-O Notation)
- Time Complexity를 표현하는 방식
- 입력 크기(n)가 증가할 때 알고리즘의 실행 시간이 얼마나 빠르게 증가하는지 표현

|시간복잡도|설명|
|:---:|---|
|O(1)<br>상수 시간(Constant Time)|알고리즘의 시행 시간이 입력 크기와 상관없이 일정|
|O(lon g)<br>로그 시간(Longarithmic Time)|입력 크기가 커질 수록 실행 시간이 완만하게 증가|
|O(n)<br>선형 시간(Linear Time)|입력 크기에 비례하여 실행 시간이 증가|
|O(n log n)<br>선형 로그 시간(Linearithmic Time)|- 선형 시간보다 더 복잡한 시간복잡도<br>- 일반적으로 효율적인 정렬 알고리즘에서 발생|
|O(n^2)<br>지수 시간(Exponential Time)|- 입력 크기가 커질수록 실행 시간이 지수적으로 증가<br>- 보통 입력 크기가 작을 때만 사용|
|O(n!)<br>팩토리얼 시간(Factorial Time)|- 입력 크기가 커질수록 실행 시간이 매우 빠르게 증가<br>- 주로 모든 가능한 순열 계산하는 알고리즘에서 발생|

### 1.2.1. Big-O Notation 예시
- O(1)
```
int getFirstEl(int[] arr) {
  return arr[0];
}
```

- O(n)
```
int sum(int[] arr) {
  int sum = 0;
  for (int num : arr) {
    sum += num;
  }
  return sum;
}
```

- O(n^2)
```
void printPairs(int[] arr) {
    for(int i = 0; i < arr.length; i++) {
        for(int j = 0; j < arr.length; j++) {
            System.out.println(arr[i] + ", " + arr[j]);
        }
    }
}
```

## 1.3. 분석 방법
- 반복문
  - 반복문이 한 번 실행될 때마다 O(n)
  - 중첩된 반복문 O(n^2), O(n^3)와 같은 더 높은 차수의 시간 복잡도를 가짐
- 조건문
  - if-else 조건문은 입력 크기에 영향을 미치지 않는 경우 o(1)
- 재귀 호출
  - 재귀 함수의 시간 복잡도는 재귀 호출의 깊이와 각 호출의 작업에 따라 달라짐
  - 피보나치 재귀 함수는 O(2^n) 시간 복잡도를 가짐
- 연산
  - 일반적인 산술 연산, 비교, 할당 등은 O(1)

# 2. Sort
- 데이터가 주어져 있을 때, 일정한 기준으로 오름차순 또는 내림차순으로 순서를 재배열하는 것
- 일반적으로 최악의 경우 O(n^2)의 시간복잡도가 소모되며, 가장 효율적인 경우 O(n log n)으로 동작
## 2.1. Selection Sort
- 최솟값을 찾아 맨 앞으로 옮겨주는 방법
- 각 원소를 하나하나 선택해서 배치하기 때문에 시간 복잡도는 O(n^2)

```
public class SelectionSort {
    public static void selectionSort(int[] arr) {
        int n = arr.length;

        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;

            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIndex]) {
                    minIndex = j;
                }
            }

            int temp = arr[minIndex];
            arr[minIndex] = arr[i];
            arr[i] = temp;
        }
    }

    public static void main(String[] args) {
        int[] data = {64, 25, 12, 22, 11};
        selectionSort(data);
    }
}
```

## 2.2. Bubble Sort
- 인접한 두 원소를 비교하여 정렬
- i번째와 i+1번째 원소를 비교해서 바꾸어주는 방식
- 과정을 n번 반복하므로 시간복잡도는 O(n^2)

```
public class BubbleSort {
    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        boolean swapped;

        for (int i = 0; i < n - 1; i++) {
            swapped = false; // 교체 발생 여부 체크

            for (int j = 0; j < n - 1 - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }

            if (!swapped) break;
        }
    }

    public static void main(String[] args) {
        int[] data = {5, 1, 4, 2, 8};
        bubbleSort(data);
    }
}
```

## 2.3. Insertion Sort
- 이미 정렬된 부분과 비교하여 정렬하는 방법
- 시간복잡도는 O(n^2)

```
public class InsertionSort {
    public static void insertionSort(int[] arr) {
        int n = arr.length;

        for (int i = 1; i < n; i++) {
            int key = arr[i];
            int j = i - 1;

            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            }

            arr[j + 1] = key;
        }
    }

    public static void main(String[] args) {
        int[] data = {8, 5, 6, 2, 4};
        insertionSort(data);
    }
}
```

## 2.4. Merge Sort
- 데이터를 두 부분으로 분할하고, 그 분할된 데이터를 계속해서 분할하는 과정을 반복한 다음 분할된 값들을 병합하면서 정렬하는 방법
1. 분할(Divide) : 배열을 더 이상 나눌 수 없을 때까지 정확히 반으로 나눈다
2. 정복(Conquer) : 각 부분 배열을 재귀적으로 정렬
3. 결합(Combine/Merge) : 정렬된 부분 배열들을 다시 하나의 정렬된 배열로 합침

<img width="1280" height="631" alt="Image" src="https://github.com/user-attachments/assets/059f5c56-3719-4c12-ba24-0f70b4696b3e" />

```
public class MergeSort {
    public static void mergeSort(int[] arr, int left, int right) {
        if (left < right) {
            int mid = (left + right) / 2;

            // 1. 분할: 왼쪽과 오른쪽을 계속 나눔
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);

            // 2. 병합: 나뉜 배열들을 정렬하며 합침
            merge(arr, left, mid, right);
        }
    }

    private static void merge(int[] arr, int left, int mid, int right) {
        int[] temp = new int[right - left + 1];
        int i = left;     // 왼쪽 부분 배열 시작점
        int j = mid + 1;  // 오른쪽 부분 배열 시작점
        int k = 0;        // 임시 배열 인덱스

        // 양쪽 배열을 비교하며 작은 순서대로 temp에 넣기
        while (i <= mid && j <= right) {
            if (arr[i] <= arr[j]) {
                temp[k++] = arr[i++];
            } else {
                temp[k++] = arr[j++];
            }
        }

        // 남은 원소들 처리 (왼쪽이나 오른쪽 한쪽이 먼저 끝난 경우)
        while (i <= mid) temp[k++] = arr[i++];
        while (j <= right) temp[k++] = arr[j++];

        // temp 배열의 내용을 원래 배열(arr)에 복사
        for (int l = 0; l < temp.length; l++) {
            arr[left + l] = temp[l];
        }
    }

    public static void main(String[] args) {
        int[] data = {38, 27, 43, 3, 9, 82, 10};
        mergeSort(data, 0, data.length - 1);
    }
}
```

## 2.5. Quick Sort
- 최악의 경우 O(n^2)이고 평균적으로 O(n log n)의 시간복잡도
1. 피벗(Pivot) 선택 : 배열에서 원소 하나를 기준(Pivot)으로 잡는다
2. 분할(Partition) : 피벗보다 작은 원소들은 왼쪽으로, 큰 원소들은 오른쪽으로 옮김
3. 재귀 : 피벗을 제외한 왼쪽과 오른쪽 배열에 대해 위 과정을 반복

```
public class QuickSort {
    public static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            // 1. 피벗을 기준으로 나누고, 피벗의 최종 위치를 받음
            int pivotIndex = partition(arr, low, high);

            // 2. 피벗 왼쪽 부분 정렬
            quickSort(arr, low, pivotIndex - 1);
            // 3. 피벗 오른쪽 부분 정렬
            quickSort(arr, pivotIndex + 1, high);
        }
    }

    private static int partition(int[] arr, int low, int high) {
        // 여기서는 가장 오른쪽 원소를 피벗으로 선택
        int pivot = arr[high];
        int i = (low - 1); // 작은 원소들이 들어갈 위치의 인덱스

        for (int j = low; j < high; j++) {
            // 현재 원소가 피벗보다 작거나 같으면
            if (arr[j] <= pivot) {
                i++;
                // i번째와 j번째 원소 교체
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // 마지막으로 피벗을 자기 위치(i+1)로 이동
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1; // 피벗의 위치 반환
    }

    public static void main(String[] args) {
        int[] data = {10, 80, 30, 90, 40, 50, 70};
        quickSort(data, 0, data.length - 1);
    }
}
```

## 2.6. Heap Sort
- Heap
  - 완전 이진 트리의 일종
  - 부모 노드의 값이 자식 노드의 값보다 항상 크거나(Max Heap), 항상 작은(Min Heap) 규칙을 가진 트리
1. 힙 구성(Build Heap) : 정렬되지 않은 배열을 최대 힙(부모가 자식보다 큰 상태)으로 만든다. 이렇게 하면 루트 노드에는 항상 최댓값이 옴
2. 추출 및 재정렬 : 루트 노트를 맨 마지막 노드와 교체, 배열의 크기를 하나 줄인 셈 치고 다시 나머지 트리 부분을 최대 힙으로 만듬, 위 과정을 반복하면 값이 큰 순서대로 뒤에서부터 쌓임

```
public class HeapSort {
    public static void heapSort(int[] arr) {
        int n = arr.length;

        // 1. 최대 힙 만들기 (Build Max Heap)
        // 부모 노드들만 대상으로 heapify 수행 (n/2 - 1부터 루트까지)
        for (int i = n / 2 - 1; i >= 0; i--) {
            heapify(arr, n, i);
        }

        // 2. 하나씩 꺼내서 정렬하기
        for (int i = n - 1; i > 0; i--) {
            // 루트(최댓값)를 현재 마지막 노드와 교체
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;

            // 크기를 줄인 힙에 대해 다시 최대 힙 구성
            heapify(arr, i, 0);
        }
    }

    // 트리를 최대 힙으로 유지하는 함수
    private static void heapify(int[] arr, int n, int i) {
        int largest = i;    // 부모
        int left = 2 * i + 1;  // 왼쪽 자식
        int right = 2 * i + 2; // 오른쪽 자식

        // 왼쪽 자식이 부모보다 크면
        if (left < n && arr[left] > arr[largest])
            largest = left;

        // 오른쪽 자식이 현재 가장 큰 값보다 크면
        if (right < n && arr[right] > arr[largest])
            largest = right;

        // 가장 큰 값이 부모가 아니라면 교체 후 재귀 호출
        if (largest != i) {
            int swap = arr[i];
            arr[i] = arr[largest];
            arr[largest] = swap;

            heapify(arr, n, largest);
        }
    }

    public static void main(String[] args) {
        int[] data = {12, 11, 13, 5, 6, 7};
        heapSort(data);
    }
}
```

# 3. Search
- 저장된 데이터들 중에서 원하는 값을 찾는 것
## 3.1. 종류
- 선형 탐색 알고리즘 (Linear Search Algorithm)
  - 왼쪽부터 순서대로 확인
  - 찾고자 하는 값을 리스트의 맨 앞에서부터 끝까지 차례대로 찾아 나가는 방식
  - 장점
    - 검색 방법 중 가장 단순하여 구현이 쉽고, 정렬되지 않은 리스트에서도 사용 가능
  - 단점
    - 검색할 리스트의 길이가 길면 비효율적

```
public int linearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) return i; // 찾으면 인덱스 반환
    }
    return -1; // 못 찾으면 -1 반환
}
```

- 이진 탐색 알고리즘 (Binary Search Algorithm)
  - 중간 지점을 기준으로 반씩 제외하는 방식
  - 오름차순으로 정렬되어 있는 리스트에서 특정한 값을 찾을 때, 처음 중간의 값을 임의의 값으로 선택하여, 그 값과 찾고자 하는 값의 크고 작음을 비교
  - 장점
    - 검색이 반복될 때마다 목표값을 찾을 확률은 두 배가 되므로 속도가 빠름
  - 단점
      - 정렬된 리스트에서만 사용 가능

```
public int binarySearch(int[] arr, int target) {
    int low = 0;
    int high = arr.length - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2; // (low + high) / 2 의 오버플로우 방지용

        if (arr[mid] == target) {
            return mid; // 찾았다!
        } else if (arr[mid] < target) {
            low = mid + 1; // 오른쪽 절반으로 범위 축소
        } else {
            high = mid - 1; // 왼쪽 절반으로 범위 축소
        }
    }
    return -1; // 존재하지 않음
}
```

***
# 참고자료
## 시간복잡도
https://www.devkobe24.com/CS/2024/2024-10-21-time-complexity.html
## Sort
https://david0506.tistory.com/4
## Search
https://daily-finn.tistory.com/61
