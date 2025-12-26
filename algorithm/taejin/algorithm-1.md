# 시간복잡도

어떠한 알고리즘의 문제를 해결하는데 걸리는 시간과 입력의 함수 관계를 가리킨다.

## 시간 복잡도 표기 방법

- Big-O: 상한 접근을 표시한다.
- Big-Ω: 하한 접근을 표시한다.
- Big-θ: 평균 접근을 표시한다.

알고리즘의 평균 접근은 구하기가 어렵고(모든 입력 사례[best, worst, average]를 구하고 평균을 구해야하기 때문에 어렵다.), <br>
하한은 "최소한 이만큼은 걸려"라는 것은 성능 최적화에 큰 도움이 되지 않기 때문에, **빅-오** 표기법을 사용한다.

## Big-O

빅-오 표기법은 계수와 낮은 차수의 항을 제외시키고, 최고 차항만 남기고 표기하는 방법이다.

> 어떤 알고리즘에 필요한 시간이 $5n^3 + 3n$ 이라면 $O(n^3)$ 이라고만 표기하면 된다.

<img width="600" height="1156" alt="image" src="https://github.com/user-attachments/assets/8f543d12-afdc-4f78-8b53-e8797dd3d742" />

## $O(1)$

가장 빠른 알고리즘으로 $O(1)$의 시간이 걸린다고도 표현하며, 입력 값이 증가하더라도 시간이 늘어나지 않고 즉시 출력 값을 얻을 수 있다.

### 예시

- 배열의 index를 활용한 참조
- 해시 충돌이 일어나지 않은 해시 테이블로 구현된 자료구조

## $O(n)$

$O(n)$시간이 걸리는 알고리즘으로, 선형 복잡도라고도 불리며 입력값이 증가함에 따라 시간 또한 **같은 비율**로 증가하는 알고리즘을 뜻한다.

### 예시

- 배열의 순차 탐색
- n번 반복하는 반복문

## $O(logn)$

$O(logn)$ 시간이 걸리는 알고리즘으로, 로그 복잡도라고도 불리며 $log_2$에서 2는 생략된 모습이다. <br>
상수 시간 다음으로 빠른 속도를 보여준다.

### 예시

- 불균형이 존재하지 않는 BST에서 값 탐색
- 힙에서 삽입과 삭제

## $O(n^2)$

$O(n^2)$ 시간이 걸리는 알고리즘으로, 2차 복잡도라고 불리며, 입력 값에 따라 시간이 **거듭 제곱**으로 증가하는 알고리즘을 뜻한다.

### 예시

- 버블 정렬과 같은 알고리즘
- 2차원 배열 전체 탐색

# Sort

모든 Sort 알고리즘을 다룰 순 없으니 Merge, Quick, Radix만 다루어 볼 예정.

## Merge Sort

## Quick Sort

## Radix Sort

# Search

탐색 알고리즘은 target 값을 자료구조에서 찾아내는 알고리즘으로 Linear와 Binary만 다루어 볼 예정.

## Linear Search

배열과 같은 자료구조에서 0번째 요소부터 마지막 요소까지 순차적으로 탐색을 진행하여, targe 값과 같다면 return해주는 알고리즘이다.

```js
function linearSearch(arr, target) {
  for (let i = 0; i < arr.length; i++) { 
    if (arr[i] === target) { 
      return i; // 찾으면 인덱스 반환
    }
  }
  return -1; // 탐색 실패
}
```

$O(n)$ 시간 복잡도를 가진다.

## Binary Search

배열을 기준으로는 반씩 targe 값과 비교하며 탐색을 진행하는 알고리즘으로 응용으로는 배열이 아닌 트리 구조를 만드는 BST가 존재한다. <br>
아래 코드 예시는 배열 기준 이진 탐색 함수

```js
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    let mid = Math.floor((left + right) / 2); // 소수점 제거를 위한 floor 사용

    // 2. 중간값과 타겟 비교
    if (arr[mid] === target) {
      return mid; // 찾았을 때 해당 인덱스 반환
    } else if (arr[mid] > target) {
      // 중간값이 타겟보다 크면, 왼쪽 절반을 탐색하기 위해 범위를 좁힘
      right = mid - 1;
    } else {
      // 중간값이 타겟보다 작면, 오른쪽 절반을 탐색하기 위해 범위를 좁힘
      left = mid + 1;
    }
  }

  return -1; // 탐색 실패
}
```

$O(logn)$의 시간 복잡도를 가진다.


# 참고 자료

## 시간 복잡도

https://hanamon.kr/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-time-complexity-%EC%8B%9C%EA%B0%84-%EB%B3%B5%EC%9E%A1%EB%8F%84/ <br>
https://ko.wikipedia.org/wiki/%EC%8B%9C%EA%B0%84_%EB%B3%B5%EC%9E%A1%EB%8F%84
