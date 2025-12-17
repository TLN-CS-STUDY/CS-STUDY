# 1. Array
- 미리 할당된 크기에 연관된 데이터를 메모리 상에 연속적이고 순차적으로 저장하는 선형 자료구조

<img width="703" height="228" src="https://github.com/user-attachments/assets/7cbef648-9973-47aa-b971-6227b6072d20" />

## 1.1. 특징
- 저장공간 고정
- 순차적 저장
- 인덱스로 원소 접근 가능
- 마지막 원소가 아닌 원소를 제거하면 인덱스를 조정하는 shifting이 일어나 O(n)만큼의 시간 소요
- lookup, append가 빨라 원소를 빈번히 조회해야하는 경우 유리
- 크기가 고정되어 있어 사용하지 않는 공간이 있을 경우 메모리 낭비 발생
- 크기가 고정되어 있어 크기를 변경하려면 새로운 배열을 만든 후 옮겨줘야 함

## 1.2. 예시코드
```
int[] arr = new int[3];
arr[0] = 1;
arr[1] = 2;
arr[2] = 3;
```

***

# 2. LinkedList
- 노드라는 구조체에 데이터값과 다음 노드의 주소를 저장하고 있는 자료구조
- 기존 배열 자료구조의 삽입/삭제 비효율성을 해소하기 위해 등장
- 데이터는 물리적으로 비연속적인 저장이지만, 각 노드들이 다음 노드의 주소를 가리키고 있으므로 논리적으로는 연속적 저장

<img width="635" height="215" src="https://github.com/user-attachments/assets/7de62ab4-477e-405a-b619-ab14fc10ab56" />

## 2.1. 특징
- 데이터가 추가되는 시점에 메모리 할당으로 효율적 사용 가능
- 데이터 이동 속도 빠름
- 데이터 조회 속도 느림 (랜덤 엑세스 불가능)
- Head 주소 기억 필요

## 2.2. 단점
- 실 연산 속도 저하
- 주소 저장으로 인한 공간 낭비
- 복잡한 연산으로 인한 오버헤드

## 2.3. 예시코드
### 2.3.1. Singly LinkedList
```
class Node {
    int data;
    Node next;

    public Node (int data) {
        this.data = data;
        this.next = null;
    }
}

class SinglyLinkedList {
    Node head;

    public SinglyLinkedList() {
        this.head = null;
    }

    public void append (int data) {
        Node node = new Node(data);

        if (head == null) {
            head = node;
            return;
        }

        Node current = head;
        while (current.next != null) {
            current = current.next;
        }

        current.next = node;
    }
}
```
### 2.3.2. Doubly LinkedList
```
class Node {
    int data;
    Node next;
    Node prev;

    public Node (int data) {
        this.data = data;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList {
    Node head;
    Node tail;

    public DoublyLinkedList() {
        this.head = null;
        this.tail = null;
    }

    public void append (int data) {
        Node node = new Node(data);

        if (head == null) {
            head = node;
            tail = node;
            return;
        }

        tail.next = node;
        node.prev = tail;
        tail = node;
    }
}
```

***

# 3. Stack
- '쌓다', '쌓이다'
- 데이터를 순서대로 쌓는 자료 구조

<img width="700" height="300" src="https://github.com/user-attachments/assets/5ef17334-ac20-4813-8743-91489cd98c1e" />

## 3.1. 특징
- LIFO(Last In First Out, 후입선출)
- 데이터의 삽입과 삭제는 top이라고 일컫는 한 쪽 끝에서만 이루어지도록 제한하여 만든 자료구조
## 3.2. 기본 연산
1. push()
- stack의 제일 위에 데이터를 추가하는 연산
2. pop()
- stack의 제일 위의 데이터를 제거하고 반환하는 연산
3. peek()
- stack의 제일 위의 데이터를 반환하는 연산
4. isEmpty()
- stack이 비어있는지 확인하는 연산
## 3.3. 장단점
- 장점
    - 간단한 구현
    - 빠른 속도
- 단점
    - 크기 제한
## 3.4. 예시코드
```
public class ArrayStack {
    int top;
    int size;
    int [] stack;

    public ArrayStack(int size) {
        this.size = size;
        stack = new int[size];
        top = -1;
    }

    public void push (int item) {
        stack[++top] = item;
    }

    public void pop () {
        int pop = stack[pop];
        stack[top--] = 0;
    }
}
```

***

# 4. Queue
- '줄을 서서 기다린다', '대기행렬'

## 4.1. 특징
- FIFO(First In First Out)
- 데이터는 하나씩 출입 가능
- 두 개의 입출력 방향

## 4.2. 기본 연산
1. add()
- Queue의 rear에 데이터 추가
2. poll()
- Queue의 front의 데이터를 제거하고 반환
- 비어있을 경우 null 반환
3. remove()
- poll()과 동일하지만 큐가 비어있으면 NoSuchElement 에러 반환
4. peek()
- Queue의 front 데이터 반환
5. isEmpty()
- Queue가 비어있는지 확인
## 4.3. 장단점
- 장점
    - 순서가 중요한 상황에 활용
    - 배열이나 연결 리스트 구현에 적합
- 단점
    - 큐에서 임의의 위치에 있는 항목에 접근 어려움
    - ㅂ열 기반의 구현에서 크기가 고정되어 있어 확정 어려움
## 4.4. 종류

| 종류 | 정의 |
| :---: | :--- |
| 선형 큐 | 일반적인 큐로, 데이터가 선형적으로 저장 <br>배열이나 연결리스트로 구현가능 |
| 원형 큐 | 선형 큐의 한 종류로, rear와 front가 순환적으로 움직임 |
| 우선순위 큐 | 각 데이터의 우선순위가 정해져 있고, 우선순위에 따라 삭제 및 검색이 이루어지는 큐 <br> Heap과 같은 자료구조 규현 |
| 덱 | 양쪽 끝에서 데이터의 삽입과 삭제가 가능한 큐로, 스택과 큐의 기능을 모두 가짐 |

***

# 5. Deque
- Double - Ended Queue
- 한쪽에서만 삽입, 다른 한쪽에서만 삭제가 가능했던 Queue와 달리 양쪽 front, rear에서 삽입/삭제가 모두 가능한 자료구조

<img width="1618" height="1026" src="https://github.com/user-attachments/assets/9e055f55-6fcc-46e4-99d0-7e2dce777b76" />

# 5.1. 기본 연산
1. create()
- 덱 생성
2. init(dq)
- 덱 초기화
3. is_empty(dq)
- 덱이 비어있는지 검사
4. is_full(dq)
- 덱이 꽉 차있는지 검사
5. add_front(dq, e)
- 덱의 앞 원소 추가
6. add_rear(dq, e)
- 덱의 뒤 운소 추가
7. delete_front(dq)
- 덱의 앞 원소 제거 및 반환
8. delete_rear(dq)
- 덱의 뒤 원소 제거 및 반환
9. pop_front(q)
- 덱의 앞 원소 반환
10. pop_rear(q)

<img width="1217" height="807" src="https://github.com/user-attachments/assets/5ca168e6-2fc9-4ffd-a18c-d9ef8e1bca0c" />
- 덱의 뒤 원소 반환

# 6. HashTable
- (Key, Value)로 데이터를 저장하는 자료구조
- 빠르게 데이터를 검색 가능

<img width="315" height="230" src="https://github.com/user-attachments/assets/e1d90c72-6c48-42c3-a9cc-254a2e42730c" />

## 6.1. Hash 함수
1. Divison Method
- 나눈셈을 이용하는 방법으로 입력값을 테이블의 크기로 나누어 계산
2. Digit Folding
- 각 Key의 문자열을 ASCII 코드로 바꾸고 값을 합한 데이터를 테이블 내의 주소로 사용
3. Multiplication Method
- 숫자로 된 Key값 K와 0과 1사이의 실수 A, 보통 2의 제곱수인 m을 사용하여 다음과 같은 계산을 해줌
- h(k) = (kAmod1) * m
4. Univeral Hashing
- 다수의 해시함수를 만들어 집합 H에 넣어두고 무작위로 해시함수를 선택해 해시값을 만드는 기법
## 6.2. Hash 값이 충동하는 경우
### 6.2.1. 분리 연결법 (Separate Chaining)
- 동일한 버킷의 데이터에 대해 자료구조를 활용해 추가 메모리를 사용하여 다음 데이터의 주소를 저장
- 장점
    - 해시 테이블의 확장이 필요없고 간단학 구현이 가능하며, 손쉽게 삭제 가능
- 단점
    - 데이터의 수가 많아지면 동일한 버킷에 chaining되는 데이터가 많아지며 그에 따라 캐시의 효율성 감소
### 6.2.2. 개방 주소법(Open Addressing)
- 추가적인 메모리를 사용하는 Chainig 방식과 다르게 비어있는 해시 테이블의 공간을 활용하는 방법
1. Linear Probing
- 현재의 버킷 index로부터 고정폭만큼씩 이동하여 차례대로 검색해 비어 있는 버킷에 데이터 저장
2. Quadratic Probing
- 해시의 저장순서 폭을 제곱으로 저장하는 방식 
3. Double Hashing Probing
- 해시된 값을 한번 더 해싱하여 해시의 규칙성을 없애버리는 방식 
- 해시된 값을 한 번 더 해싱하여 새로운 주소를 할당하기 때문에 다른 방법들보다 많은 연산 소요

***

# 7. Heap Tree
- 배열의 원소를 정렬하기 위한 구조
## 7.1. Heap
### 7.1.1. Max Heap
- 각 노드의 키값이 그 자식의 키값보다 작지 않은 트리
- 최대 트리(Max Tree) 이면서 완전 이진 트리(Complete Binary Tree)
### 7.1.2. Min Heap
- 각 노드의 키 값이 그 자식의 키값보다 크지 않은 트리
- 최소 트리(Min Tree) 이면서 완전 이진 트리(Complete Binary Tree)
### 7.1.3. Complete Binary Tree
- 두 개의 자식 노드만 갖는 이진 트리 중 노드가 왼쪽부터 차례대로 채워져 있는 트리

<img width="840" height="432" src="https://github.com/user-attachments/assets/550ca68e-1be0-43c8-9478-67990658fe34" />

## 7.2. 장단점
- 장점
    - 빠른 삽입 및 삭제
    - 우선 순위 기반 작업 처리
- 단점
    - 임의 접근 어려움
    - 정렬 유지의 오버헤드
    - 배열로 구현 시 추가적인 공간 요구

## 7.3. Heap의 응용 
1. 우선순위 큐(Priority Queue)
- 요소가 들어온 순서가 아니라 우선 순위에 따라 처리되며, Heap은 최댓값 또는 최솟값을 효율적으로 관리하는데 유리
- 기본적으로 오름차순으로 동작하며, 사용자가 정의한 우선순위로 정렬 가능
2. 힙 정렬(Heap Sort)
- 정렬 알고리즘으로, 최대 힙이나 최소 힙을 구성한 후, 루트 노드를 제거하고 재정렬하는 과정을 반복해 정렬을 수행
- 비교 기반 정렬 알고리즘 중 효율적
- 제자리 정렬이 가능하지만 안정적인 정렬은 아니다
3. 다익스트라 알고리즘(Dijkstra's Algorithm)
- 최단 경로 알고리즘 중 하나로, 우선순위 큐를 사용해 가중치가 있는 그래프에서 최단 경로를 찾음
- 이 과정에서 최소 힙이 사용되어, 현재까지 가장 작은 거리를 가진 정점을 효율적으로 선택 가능
4. 이진 힙(Binary Heap)과 페어링 힙(Pairing Heap)
- 이진 힙은 가장 기본적인 형태이고, 페어링 힙은 더 복잡하지만 삽입과 삭제가 효율적

***
# 참고자료
## Array
https://velog.io/@newdana01/CS-Array%EC%99%80-LinkedList-%EC%A0%95%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90
## LinkedList
https://hoehen-flug.tistory.com/29
https://mongsil-jeong.tistory.com/58
## Stack
https://velog.io/@rlvy98/CS-%EC%8A%A4%ED%83%9DStack
## Queue
https://jyunslog.tistory.com/
## Deque
https://velog.io/@nnnyeong/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%8A%A4%ED%83%9D-Stack-%ED%81%90-Queue-%EB%8D%B1-Deque
https://laurent.tistory.com/entry/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EB%8D%B1-Deque
## HashTable
https://mangkyu.tistory.com/102
## Tree
https://velog.io/@redgem92/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%9E%99-%ED%8A%B8%EB%A6%ACHeap-Tree
https://juhee-maeng.tistory.com/entry/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%9E%99Heap%EC%9D%B4%EB%9E%80-%EC%B5%9C%EB%8C%80%ED%9E%99Max-Heap%EA%B3%BC-%EC%B5%9C%EC%86%8C%ED%9E%99Min-Heap
