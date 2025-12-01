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



***
# 참고자료
## Array
https://velog.io/@newdana01/CS-Array%EC%99%80-LinkedList-%EC%A0%95%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90
## LinkedList
https://hoehen-flug.tistory.com/29
https://mongsil-jeong.tistory.com/58
