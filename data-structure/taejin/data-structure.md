# Array

**정의:** 동일한 타입의 데이터를 메모리 상에 연속적으로 저장하는 자료구조.

**특징:**
- 고정 크기이다.
- 연속된 메모리 공간에 존재하므로, 캐시 효율이 좋다.

**Time Complexity**:

| operation | avg case time complexity | worst case time complexity |
| :---: | :---: | :---: |
| insertion / deletion / search | $O(n)$ | $O(n)$ |

#  Linked List

<img width="640" height="123" alt="image" src="https://github.com/user-attachments/assets/551e1638-d979-4c86-a77d-618dcf2234b7" />

**정의**: 데이터와 포인터로 구성된 노드간의 연결을 사용해서 리스트로 구현한 자료구조이다. <br> _(배열의 고정크기 단점을 보완 + 삽입/삭제 용이)_

**특징:**
- 가변 크기이다.
    - 데이터 추가/삭제 시 메모리를 동적으로 할당/해제하므로 크기 제한이 유연하다.
- 데이터 외에 주소 값을 저장할 공간이 추가로 필요하다. (`next`, `prev`)
- `[Data | Next]` 형태의 노드로 구성된다.

**Time Complexity**:

| operation | avg case time complexity |
| :---: | :---: |
| HEAD에 대한 insertion / deletion | $O(1)$ |
| TAIL에 대한 insertion / deletion | $O(1)$ : TAIL 위치를 아는 경우 <br> $O(n)$: TAIL 위치 모르는 경우 |
| (중간 위치) insertion / deletion | $serach time + O(1)$ <br> (삽입할 위치까지 탐색 + next pointer 변경) |

## Double Linked list

<img width="640" height="242" alt="image" src="https://github.com/user-attachments/assets/55affefe-08cb-4b09-bd42-4477444db2b0" />

**특징**:
- 기존 single linked list는 next로만 탐색이 가능하다는 단점을 보완하기 위해 만들어짐
  - prev를 이용해 더 빠르게 접근 가능해짐
- 양방향 연결 `[Prev | Data | Next]`
- 주소 추가에 따른 메모리를 더 쓴다.

## Circular Linked List

<img width="640" height="356" alt="image" src="https://github.com/user-attachments/assets/91a9611f-5e62-44fe-95ea-8356348e5450" />

**특징:**
- HEAD와 TAIL을 연결한 것이다.
    - TAIL의 next를 null이 아닌 HEAD로 표시

# Stack

<img width="400" height="600" alt="image" src="https://github.com/user-attachments/assets/0c739cb6-c9d9-420c-ac2d-e7847cc9652c" />

**정의:** LIFO 자료구조로 한쪽 끝에서만 삽입/삭제가 가능한 자료구조이다.

**Method**:
- push(x): Top에 data를 삽입
- pop(): Top의 data를 반환 및 삭제
- peek(): Top을 반환 (삭제는 안함)
- isEmpty(): 스택이 비어있는지 확인

**Time Complexity**:

| operation | avg case time complexity |
| :---: | :---: |
| insertion / deletion | $O(1)$ |
| search | $O(n)$ |

push와 pop, peek는 top에 대한 연산이 이루어 지므로 $O(1)$이다. <br>
하지만 탐색은 top부터 순차 탐색을 진행해야하므로 $O(n)$이다.

**Implementation:**
- array
  ```js
  TODO
  ```
- linked list
  ```js
  TODO
  ```

**활용:**

- 함수 재귀 호출
- undo와 같은 뒤로가기 기능
- 메모리의 스택 영역 등등…

# Queue

<img width="600" height="397" alt="image" src="https://github.com/user-attachments/assets/098ca633-95d6-412a-9521-e2004d29ea4c" />

**정의:** FIFO 자료구조로 한쪽 끝에서 IN(rear), 다른 쪽(front)에서 OUT이 이루어진다.

**Method:**
- enque(x): rear에 data 추가
- deque(): front에서 data 제거
- peek(): front에 있는 항목을 반환
- isFull(): 큐가 가득 찾는지 확인
- isEmpty(): 큐가 비어있는지 확인

**Time Complexity**:

| operation | avg case time complexity 
| :---: | :---: |
| Access / Search | $O(n)$ |
| enqueue | $O(1)$ |
| dequeue | $O(1)$ |

**Implementation:**
- array
  ```js
  TODO
  ```
- linked list
  ```js
  TODO
  ```

**활용:**
- 스케줄링 처리 (들어온 순서대로)
- 등등…

## Circular Queue

<img width="600" height="571" alt="image" src="https://github.com/user-attachments/assets/bb7d7b53-1145-4888-b3f5-257f8be25226" />

**정의:** array 기반으로 큐를 만들 경우 크기 문제가 발생하는데, 이를 보완하기 위해 원형처럼 만들어서 순환하게 만든 큐 <br> _(실제로 원형은 아님)_

**특징:**
- 배열의 끝에 도달하면 다시 배열의 처음으로 돌아가 데이터가 저장되므로 배열의 공간을 효율적으로 사용할 수 있다.
  - `rear++;` 이 아니라 `(rear+1)%(MAX_SIZE);`로 rear 값을 update해준다.

## Deque

<img width="600" height="548" alt="image" src="https://github.com/user-attachments/assets/6780902c-4c3c-4714-98e7-364e8680d9b5" />

**정의:** 양방향 큐로 즉, 양쪽에서 삽입과 삭제 연산이 가능해지는 것이다.

**Method:**
- addFront(x): Front에 data 추가
- addRear(x): Rear에 data 추가
- deleteFront(): Front에서 data 제거
- deleteRear(): Rear에서 data 제거
- getFront(): Front에 있는 항목을 반환
- getRear(): Rear에 있는 항목을 반환
- isFull(): 덱이 가득 찾는지 확인
- isEmpty(): 덱이 비어있는지 확인

**Implementation:**
- array
  ```js
  TODO
  ```
- linked list
  ```js
  TODO
  ```

# Hash Table

<img width="300" height="230" alt="image" src="https://github.com/user-attachments/assets/5e0d96c8-2d76-4a4a-85d3-a389f1099516" />

**정의:** `key: value` 형태로 data를 저장하는 자료구조이다.

**특징**:
- O(1)의 빠른 검색 속도를 제공한다.
- key값에 해시 함수를 적용해 배열의 고유한 index를 생성하고 이 index값을 사용해 저장하거나 검색한다.
    - index값을 저장하는 장소를 buckets 또는 slots이라고 한다.
- buckets을 추가로 만들어야 하므로 추가적인 메모리 사용이 존재한다.

**Time Complexity**:

| operation | avg case time complexity | worst case time complexity |
| :---: | :---: | :---: |
| search/insert/deletion | $O(1)$ | $O(n)$ |

**worst case time complex:**
- hash값의 충돌(해시 값 중복)이 일어난 경우가 최악의 경우이며, 이를 해결하기 위한 방법은 chaining과 open addressing 방식이 존재한다.

## chaining

<img width="400" height="310" alt="image" src="https://github.com/user-attachments/assets/314b145a-e1e1-4a63-8dfb-935a174821fe" />

- 동일한 버킷에 접근한다면 그 뒤의 주소로 chaining 하여 관리를 한다. <br>
_(연결 리스트와 비슷함)_
- 데이터의 수가 많아지면 해싱을 해도 $O(n)$에 가까워진다. <br>
해시 값을 타고 가도 순차 탐색(linked list)를 진행하게 되기 때문

## Open addressing

이 방식은 해시 테이블에 바로 데이터 저장이 가능하다.

대표적으로 3가지 방식이 존재하는데

### 1. Linear probing

- 충돌이 발생하는 경우(버킷에 이미 데이터가 존재한다면)에 다음 버킷으로 이동하여 빈 공간을 찾아낸다.
  - `hash(x) % S`가 full이면,  `hash(x+1) % S` 를 시도한다. <br> (NULL을 찾을 때 까지 x+2, x+3...반복)

### 2. Quadratic probing

- 충돌이 발생하는 경우 i번째 반복에서 $i^2$ 번째 슬롯을 찾는 방식이다.
  - `hash(x) % S`가 full이면, `(hash(x)+1*1) % S`를 시도한다. <br> (NULL을 찾을 때 까지 2*2, 3*3... 반복)

**3. Double hashing probing**

- 해시의 값을 한번 더 해싱하여 해시의 규칙성을 없애버리는 방식이다.
  - `hash(x) % S`가 full이면, `(hash(x) + 1*hash2(x) % S` 를 시도한다. <br> (NULL을 찾을 때 까지 `(hash(x) + 2*hash2(x)) % S` ... 반복)

## 해시함수 예시

이렇게 해시값을 만들어내는 해시 함수들의 종류는 아래와 같다.

### 1. Division Method

- mod 연산을 통해 해시값을 생성 (`h(x)=x%m`)

### 2. Multiplication Method

- 곱하기 연산을 통해 해시 값을 생성 (`h(x)=(x*A mod1)*m의 정수부`)

활용:
- DBMS 인덱스 관리
- Page Table
- 비밀번호 시스템 등등...

# Map

```js
const myMap = new Map();

// 추가
myMap.set('name', 'taejin');
myMap.set('age', 25);

// 조회
console.log(myMap.get('name')); // 'taejin'

// 확인
console.log(myMap.has('age')); // true

// 삭제
myMap.delete('age');

```

**정의** key와 value로 이루어진 추상 자료구조이다.

**특징:**
- 각 key는 map 내에서 유일하다.
- key는 하나의 value와 mapping된다.
- Hash Table, Search Tree 등으로 표현 가능하다.

**활용**: 
- JSON: Key-Value 구조의 데이터 교환 포맷.(자료 구조도 아니고 언어도 아님)
- NoSQL DB: Redis, MongoDB 등에서 데이터를 저장하는 기본 구조.
- 캐싱(Caching): 빠른 검색 속도를 이용해 데이터를 임시 저장할 때.

## Map vs Object

**Object**:
```js
const obj = {
    name: 'taejin',
    age: 25,
    1: 'One' // Key는 자동으로 문자열 "1"로 변환됨
};

// 접근
console.log(obj.name); // 'taejin'
console.log(obj['age']); // 25
```

Map과 비슷해 보이지만 아래의 단점이 존재한다.
1. Key는 string 또는 symbol만 가능 ([symbol이란](https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EC%9E%90%EB%A3%8C%ED%98%95-Symbol-%F0%9F%9A%A9-%EC%A0%95%EB%A6%AC))
2. 순서를 보장하지 않음 (브라우저마다 다를 수 있었음)

| 특징 | Map | Object |
|:---:|:---:|:---:|
| Key 타입 | 모든 타입 가능 (객체, 함수 등 포함) | 문자열 또는 Symbol만 가능 |
| 순서 보장 | 삽입된 순서를 보장함 (Iterable) | 순서를 보장하지 않음 (엔진마다 다를 수 있음) |
| 크기 확인 | map.size로 즉시 확인 가능 ($O(1)$) | Object.keys(obj).length로 계산 필요 ($O(n)$) |
| 성능 | 잦은 추가/삭제 시 최적화되어 있음 | 데이터가 정적이고 구조가 잡혀있을 때 유리함 |

# Tree

<img width="400" height="732" alt="image" src="https://github.com/user-attachments/assets/9df94857-b64d-4550-8fc1-33b00280414e" />

**정의:** 그래프의 한 종류로 cycle이 존재하지 않는 계층적 자료구조로 node와 node들을 연결하는 edge로 구성되어 있다.

**특징::**

- 방향이 존재한다.
- 하나의 root node만 존재한다.
- node의 개수가 $N$인 tree의 edge 수는 항상 $N-1$이다.
- 이진트리, 이진 탐색 트리, 균형 트리, 다차원 탐색 트리, 힙과 같은 종류가 있다.

## Heap

<img width="400" height="711" alt="image" src="https://github.com/user-attachments/assets/f32f3e52-45fc-4841-a80a-648b323be45e" />

**정의:** 완전이진트리의 일종으로 우선순위 큐를 위해 만들어진 자료구조이다.

**특징:**
- 우선순위를 정렬한 방식에 따라 최대 힙, 최소 힙으로 나뉜다.
  - 최대 힙:
    - 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리
    - key(부모 노드) >= key(자식 노드)
  - 최소 힙:
    - 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리
    - key(부모 노드) <= key(자식 노드)

**시간 복잡도**
|Operation|avg case time complexity|
|:---:|:---:|
|insertion / deletion | $O(logn)$

### insertion

<img width="400" height="2444" alt="image" src="https://github.com/user-attachments/assets/3ad1d2d5-a0b5-4de4-ae76-13f24d4fcaf6" />

_(이미지에서는 Max Heap으로 예시)_
insetion은 leaf node에서 이루어지며, 이후 부모 노드와의 key 값 비교를 통해 힙의 균형을 맞춘다.

### deletion

<img width="400" height="2444" alt="image" src="https://github.com/user-attachments/assets/fd3949c4-1c5b-4801-ae89-fb4c8b4635f8" />

_(이미지에서는 Max Heap으로 예시)_
Max Heap에서 deletion은 root node의 삭제를 의미하는 것으로(Min Heap에선 반대), root node 삭제 후 root node의 빈 자리를 마지막 leaf node로 replace한다. <br>
이후 자식노드와의 key 값 비교를 통해 힙의 균형을 맞춘다.

### Priority Queue

**정의:** 기존 큐의 특징인 FIFO가 아니라 우선순위대로 처리하는 큐, 위에서 설명한 Heap을 사용해 구현한다.

**Time Complexity:** <br>
_힙을 사용하여 구현하는 이유는 time complexity 측면에서 Heap으로 구현하는게 제일 효율적이라 그렇다._

|Implementation using|`enqueue()` time complexity|`dequeue` time complexity|
|:---:|:---:|:---:|
|array|$O(1)$|$O(n)$|
|linked list|$O(n)$|$O(1)$|
|heap|$O(logn)$|$O(logn)$|

# 참고자료

## Array

https://yoongrammer.tistory.com/43

## Linked List

https://yoongrammer.tistory.com/44 <br>
https://limecoding.tistory.com/90 <br>
https://opentutorials.org/module/1335/8940

## Stack

https://velog.io/@alkwen0996/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%8A%A4%ED%83%9DStack#%EC%8A%A4%ED%83%9D-%EC%8B%9C%EA%B0%84%EB%B3%B5%EC%9E%A1%EB%8F%84

## Queue

https://yoongrammer.tistory.com/46 <br>
https://velog.io/@9e0na/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EB%8D%B1DEQUE

## Hash Table

https://dayzen1258.tistory.com/entry/%ED%95%B4%EC%8B%9C%ED%85%8C%EC%9D%B4%EB%B8%94%EC%9D%B4%EB%9E%80 <br>
https://choi-records.tistory.com/entry/Data-Structure-Hash-Table#toc31 <br>
https://www.geeksforgeeks.org/dsa/open-addressing-collision-handling-technique-in-hashing/

## Map

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Map

## Tree
https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html

## Heap
https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html
