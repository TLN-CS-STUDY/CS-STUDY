배열/연결리스트
스택/큐/덱
해시테이블
트리
힙

# 1. Array
## 1.1. Array 란?
<img width="750" height="245" alt="Image" src="https://github.com/user-attachments/assets/e5c04dd6-5829-4e0b-a8f0-5a3593672034" />

- 동일한 데이터 타입의 요소들을 연속된 메모리 공간에 저장하는 방법이다.
- 배열을 구성하는 각각의 값을 요소(element), 배열에서 위치를 가리키는 숫자를 인덱스(index)라고 한다.
- 메모리 상에서 연속적으로 저장되어 있는 특징을 갖기 때문에, index를 통한 접근이 용이하다.
- 배열의 크기는 처음 생성할 때 정하며 이후에는 변경할 수 없다.

## 1.2. 특징
#### 장점
- **빠른 접근**: 인덱스를 사용하여 배열 내의 특정 요소에 빠르게 접근할 수 있다.
- **메모리 사용**: 연속된 메모리 공간에 요소를 저장하므로, 캐시 효율성이 높다.
- **간단한 구조**: 간단하고 직관적인 구조를 가진다.

#### 단점
- **크기 제한**: 배열의 크기가 고정되어 있어, 크기를 동적으로 변경하기 어렵다
- **메모리 할당 문제**: 배열의 크기가 고정되어 있어, 초기에 큰 배열을 할당하더라도 실제로 사용하는 메모리의 크기가 작을 수 있다.
- **삽입 / 삭제의 어려움**: 중간에 요소를 삽입 및 삭제할 때 다른 요소들을 이동시켜야하는 번거로움이 있다.

#### 활용
- 빠른 접근이 요구되고, 데이터 삽입과 삭제가 적을 때 사용된다.

## 1.3. 시간 복잡도
- 탐색
    - 접근하고자 하는 인덱스를 아는 경우: O(1)
    - 인덱스를 알지 못해 순차적으로 탐색하는 경우: O(n)
- 삽입 / 삭제
    - 배열의 처음 또는 중간에 삽입 및 삭제하는 경우: O(n)
    - 배열의 끝에 삽입 및 삭제하는 경우: O(1)

* * *
# 2. Linked List
## 2.1. Linked List 란?
<img width="650" height="177" alt="Image" src="https://github.com/user-attachments/assets/8a903550-8232-4e02-aca5-15b7e65df428" />

- 여러 개의 노드들이 순차적으로 연결된 형태이다.
- 첫 번째 노드를 head, 마지막 노드를 tail이라고 한다.
- 각 노드는 데이터와 다음 노드를 가리키는 포인터로 이루어져 있다.
- 배열과 다르게 메모리를 연속적으로 사용하지 않는다.
- 순차적으로 접근해야 할 때는 불리할 수 있으나, 삽입/삭제에는 용이하다.

## 2.2. Linked List의 구분
#### Singly Linked Linear List
<img width="450" height="128" alt="Image" src="https://github.com/user-attachments/assets/48a4de64-69b6-4109-a807-70c2e2a7802a" />

- 각 노드에 자료 공간과 한 개의 포인터 공간이 있고, 각 노드의 포인터는 다음 노드를 가리킨다.

#### Doubly Linked Linear List
<img width="650" height="86" alt="Image" src="https://github.com/user-attachments/assets/2646bb51-1a72-46e7-8a15-b7e67eb659ee" />

- 단일 연결 리스트와 비슷하지만, 포인터 공간이 두 개가 있고 각 포인터는 앞 / 뒤 노드를 가리킨다.

#### Circularyly Linked Linear List
<img width="400" height="219" alt="Image" src="https://github.com/user-attachments/assets/9e1a5838-da4b-4e64-89fb-23af721100d9" />

- 일반적인 Linked List에 마지막 노드와 처음 노드를 연결시켜 원형으로 만든 구조이다.

## 2.3. 특징

#### 장점
- **동적 크기**: 동적으로 크기를 변경할 수 있다.
- **삽입 / 삭제**: 특정 위치에 요소를 삽입 및 삭제 시, 인접 요소들의 이동이 필요하지 않아 해당 연산이 상대적으로 빠를 수 있다.
- **메모리 효율성**: 필요한 만큼의 메모리만 할당하므로, 메모리의 효율적인 사용이 가능하다.

#### 단점
- **접근 시간**: 임의 접근이 불가능하여, 특정 요소에 접근하기 위해서 전체 리스트를 탐색해야 할 수 있다.
- **추가적인 메모리 사용**: 각 요소마다 다음 노드를 가리키는 포인터가 필요하므로, 추가적인 메모리 사용이 발생한다.
- **캐시 비효율성**: 포인터를 통해 다음 요소를 참조하므로, 캐시 효율성이 떨어질 수 있다.

#### 활용
- 삽입과 삭제 연산이 잦고, 검색 빈도가 적을 때 사용한다.

## 2.4. 시간 복잡도
- 탐색: O(n)
- 삽입 / 삭제
    - 연결 리시트의 처음에 삽입 및 삭제하는 경우: O(1)
    - 연결 리스트의 중간에 삽입 및 삭제하는 경우: O(n) (탐색시간 소요)
    - 연결 리스트의 끝에 삽입 및 삭제하는 경우
        - 끝을 가리키는 별도의 포인터가 있는 경우: O(1)
        - 끝을 가리키는 별도의 포인터가 없는 경우: O(n)

* * *
# 3. Stack
## 3.1. Stack 이란?
<img width="450" height="1350" alt="Image" src="https://github.com/user-attachments/assets/6cbe8008-1bab-48dc-acd9-dc68168b638f" />

- 한 쪽 끝에서만 자료를 넣고 빼는 작업이 이루어지는 형태이다.
- LIFO(Last In First Out) 방식으로 동작한다.
- Push는 top에 데이터를 넣는 행위, Pop은 top의 데이터를 빼는 행위이다.
- Stack의 모든 연산(Push/POP)은 스택의 최상단인 top에서 이루어진다.
- empty일 때 pop을 시도할 경우에는 stack underflow, full일 때 push를 시도할 경우에는 stack overflow가 발생한다.

## 3.2. 특징

#### 장점
- top을 통해 접근하기 때문에 데이터 접근, 삽입, 삭제가 빠르다.

#### 단점
- top 이외의 데이터에 접근할 수 없기 때문에 탐색이 불가능하다. 탐색하기 위해서는 모든 데이터를 꺼내면서 진행해야 한다.

#### 활용
- 재귀 알고리즘
- DFS 알고리즘
- 작업 실행 취소와 같은 역추적 작업이 필요하거나 괄호 검사, 후위 연산법, 문자열 역순 출력 등에 사용한다.

## 3.3. Stack의 연산
- push(): 데이터 삽입
- pop(): 데이터 삭제
- is_empty(): 스택이 공백 상태인지 검사
- is_full(): 스택이 포화 상태인지 검사
- peek(s): 요소를 스택에서 삭제하지 않고 보기만 하는 연산

## 3.4. 시간 복잡도
- 삽입 / 삭제: O(1)
* * *
# 4. Queue
## 4.1. Queue 란?
<img width="450" height="502" alt="Image" src="https://github.com/user-attachments/assets/fe7326d5-1566-4c2f-89e7-d2a9301ad268" />

- 양 쪽 끝에서 데이터의 삽입과 삭제가 이루어지는 형태이다.
- FIFO(First In First Out) 방식으로 동작한다.
- 데이터가 삽입되는 곳을 rear, 데이터가 제거되는 곳을 front라고 한다.
- 데이터 삽입 및 삭제 전에는 Queue의 Empty/Full 여부를 확인 후 진행해야 한다.

## 4.2. Queue의 구분
#### Linear Queue
<img width="850" height="196" alt="Image" src="https://github.com/user-attachments/assets/77ad70c6-1002-4b12-bcd9-e2810b855892" />

- 선형 배열을 사용하여 구현된 Queue이다.
- 삽입을 위해서는 계속해서 요소들을 이동시켜야 한다.
- front/rear는 증가만 하는 방식으로, 실제로 front 앞 쪽에 공간이 있더라도 삽입할 수 없는 경우가 발생할 수 있다.

#### Circular Queue
<img width="650" height="1264" alt="Image" src="https://github.com/user-attachments/assets/9785dbb6-f32f-42d2-ab25-12e4e56a61b1" />

- Linear Queue의 단점을 보완한 형태이다.
- front는 첫 번째 요소 바로 앞을 rear는 마지막 요소를 가리킨다.
- Empty / Full 상태를 구분하기 위해 하나의 공간을 비워둔다.

## 4.3. 특징
#### 장점
- 데이터 접근, 삽입, 삭제가 빠르다.

#### 단점
- 중간에 위치한 데이터에 대한 접근이 불가능하다.

#### 활용
- BFS 알고리즘
- 데이터를 입력된 순서대로 처리해야 할 때 또는 프로세스 관리, 대기 순서 관리 등에 사용한다.

## 4.4. Queue의 연산
- init(): 초기화
- enqueue(e): 주어진 요소 e를 Queue의 맨 뒤에 추가
- dequeue(): Queue가 비어있지 않으면 맨 앞 요소를 삭제하고 반환
- is_empty: Queue가 비어있으면 true, 아니면 false 반환
- peek(): Queue가 비어있지 않으면 맨 앞 요소를 삭제하지 않고 반환
- is_full(): Queue가 가득 차 있으면 ture, 아니면 false 반환
- size(): Queue의 모든 요소들의 개수를 반환

## 4.5. 시간 복잡도
- 삽입 / 삭제: O(1)
* * *
# 5. Deque
## 5.1. Deque 이란?
<img width="450" height="1026" alt="Image" src="https://github.com/user-attachments/assets/8462e065-34b5-4325-9ed9-c98c312e639e" />

- **Double - Ended Queue**의 줄임말로, 양쪽 끝인 front, rear에서 삽입/삭제가 모두 가능한 형태이다.
- 연속적인 메모리를 기반으로 하는 시퀀스 컨테이너로, 가변적 크기를 갖는다.
- 중간에 데이터가 삽입될 때 다른 요소들을 앞, 뒤로 밀 수 있다.

## 5.2. 특징
#### 장점
- 데이터의 삽입/삭제가 빠르고 앞, 뒤에서 삽입/삭제가 모두 가능하다.
- 가변적인 크기를 갖는다.
- index를 통해 임의의 요소에 바로 접근이 가능하고 새로운 요소 삽입 시, 새로운 단위의 메모리 블록을 할당하여 삽입한다.

### 5.2.2. 단점
- 중간에서 삽입/삭제가 어렵고 스택,큐에 비해 비교적 구현이 어렵다.

#### 활용
- 데이터를 앞, 뒤쪽에서 모두 삽입/삭제하는 과정이 필요한 경우 또는 데이터의 크기가 가변적일 때 사용한다.

## 5.3. 시간 복잡도
- 탐색: O(1)
- 삽입 / 삭제: O(1)
* * *
# 6. Hash Table
## 6.1. Hash Table 이란?
<img width="450" height="230" alt="Image" src="https://github.com/user-attachments/assets/53a7bd29-61d2-4af6-b711-db1d7afe2ce7" />

- Key를 **Hash Function**을 통해 Hash Value로 변환하고, 이를 인덱스로 사용하여 데이터를 저장하는 Key-Value 매핑 방식이다.
- 빠른 검색, 삽입, 삭제가 가능하다.

##### ※ Hash Function?
- 주어진 데이터를 고정 길이의 불규칙한 숫자로 변환하는 함수이다.
- 대표적인 알고리즘으로 SHA가 있다.

## 6.2. Hash Collision
- Hash Function이 서로 다른 Key에 대해 같은 Hash 값을 반환함으로써 Hash Table의 같은 위치에 두 개 이상의 데이터가 저장되려는 현상이다.
- 대표적인 충돌 해결 방법에는 두 가지가 있다.

#### Chaining
- 같은 Hash 값을 가지는 데이터들을 Linked List 또는 Tree를 사용하여 저장하는 방식이다.
- Hash Table의 확장이 필요없고 간단하게 구현이 가능하며, 쉽게 삭제할 수 있다.

#### Open Addressing
- Hash Table의 다른 빈 공간을 찾아 데이터를 저장하는 방식이다.

## 6.3. 특징
#### 장점
- 검색 속도가 빠르다.
- Key를 기준으로 데이터를 저장하므로, 중복 검사 과정이 매우 빠르고 간단하다.
- 유연한 Key-Value 저장과 동적으로 크기 조절이 가능하다.
    - 다양한 타입의 데이터를 저장할 수 있다.
    - Linked List를 사용하므로, 저장할 데이터 수가 정해져 있지 않더라도 유연한 대응이 가능하다.

#### 단점
- 해시 함수가 동일한 Hash 값을 생성하거나, 배열의 크기가 너무 작으면 충돌(Collision)이 많아져 선형 탐색 빈도가 높아진다.
- 배열 기반이므로 사용되지 않는 공간이 생길 가능성이 높다.
- 데이터 삽입 순서를 보장하지 않는다.
- 특정 주소에 데이터가 몰려 성능이 저하될 수 있으므로 해시 함수가 데이터를 균등하게 분배하도록 해야 한다.

#### 활용
- 데이터베이스 인덱싱, 캐싱 시스템에 사용한다.

## 6.4. 시간 복잡도
- 탐색: O(1)
- 삽입 / 삭제: O(1)
- 데이터의 충돌이 자주 발생할 경우 O(n)이 될 수 있다.
* * *
# 7. Tree
## 7.1. Tree 란?
- 부모-자식 관계의 노드들로 이루어져 있는 비선형 계층적 자료구조이다.
- 하나의 루트 노드를 가지고, 루트 노드는 0개 이상의 자식 노드를 갖는다.
- node들과 node들을 연결하는 edge들로 구성되어 있다.

<img width="650" height="732" alt="Image" src="https://github.com/user-attachments/assets/d4d1e2c9-6419-4c71-96c3-f229e1f5d9c2" />

- 루트 노드(root node): 부모가 없는 노드, 트리는 하나의 루트 노드만을 가진다.
- 외부 노드(external node): 자식이 없는 노드이다. (= 단말 노드, leaf node)
- 내부 노드(internal node): 자식 노드 하나 이상 가진 노드이다. (= 비단말 노드, branch node)
- 간선(edge): 노드를 연결하는 선, 'link' 또는 'branch'라고도 부른다.
- 형제(sibling): 같은 부모를 가지는 노드이다.
- 깊이(depth): 루트에서 어떤 노드에 도달하기 위해 거쳐야 하는 간선의 수이다.
- 높이(height): 루트 노드에서 가장 깊숙히 있는 노드의 깊이이다.
- Size: 자신을 포함한 모든 자손 노드의 개수이다.
- Level: 트리의 특정 깊이를 가지는 노드의 집합이다.
- Degree: 노드의 자식 수이다.

## 7.2. 특징
- 하나의 루트 노드와 0개 이상의 하위 트리로 구성되어 있다.
- 데이터를 순차적으로 저장하지 않기 때문에 비선형 자료구조이다.
- 트리 내에 또 다른 트리가 있는 재귀적 자료구조이다.
- 단순 순환(Loop)를 갖지 않고, 연결된 무방향 그래프 구조이다.
- 노드 간에 부모 자식 관계를 갖고 있는 계층형 자료구조이며, 모든 자식 노드는 하나의 부모 노드만 갖는다.
- 노드가 n개인 트리는 항상 n-1개인 간선(edge)을 가진다.

# 8. Heap
## 8.1. Heap 이란?
- 완전 이진 트리의 일종으로 우선순위 Queue를 위해 만들어진 자료구조이다.
- 여러 개의 값들 중에서 최댓값이나 최솟값을 빠르게 찾아내도록 만들어졌다.
- 일종의 반정령 상태(느슨한 정렬 상태)를 유지한다.
- 중복된 값을 허용한다.

## 8.2. Heap의 종류

<img width="650" height="711" alt="Image" src="https://github.com/user-attachments/assets/3d23a1a1-fb23-476f-844b-c11e9a9f2d9b" />

- **최대 힙(max heap)**
    - 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리
    - key(부모 노드) ≥ key(자식 노드)
- **최소 힙(min heap)**
    - 부모 노드의 키 값이 자식 노드의  키 값보다 작거나 같은 완전 이진 트리
    - key(부모 노드) ≤ key(자식 노드)

## 8.3. Heap의 특징
- 보통 배열을 이용하여 구현한다.
- 구현을 쉽게 하기 위해서 인덱스 1부터 시작한다.

<img width="650" height="997" alt="Image" src="https://github.com/user-attachments/assets/f2fe17ce-eb69-46ad-8bcf-cd9772594a80" />

- 인덱스
    - 왼쪽 자식의 인덱스: [부모 인덱스] * 2
    - 오른쪽 자식의 인덱스: [부모 인덱스] * 2 + 1
    - 부모의 인덱스: [자식 인덱스] / 2

## 8.4. 시간 복잡도
- 삽입 / 삭제: O(logN)


* * *
**배열/연결리스트** <br>
https://velog.io/@xxhaileypark/%EC%9E%90%EB%A3%8C-%EA%B5%AC%EC%A1%B0-%EB%B0%B0%EC%97%B4-%EC%97%B0%EA%B2%B0-%EB%A6%AC%EC%8A%A4%ED%8A%B8-Array-LinkedList <br>
https://salt-yoo.tistory.com/10#google_vignette <br>
https://yoongrammer.tistory.com/44 <br>

**스택/큐/덱** <br>
https://velog.io/@nnnyeong/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%8A%A4%ED%83%9D-Stack-%ED%81%90-Queue-%EB%8D%B1-Deque <br>
https://comdolidol-i.tistory.com/44 <br>
https://comdolidol-i.tistory.com/47 <br>
https://bigsong.tistory.com/32 <br>


**해시테이블**
https://mojing.tistory.com/entry/Data-Structure-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%95%B4%EC%8B%9C-%ED%85%8C%EC%9D%B4%EB%B8%94Hash-Table <br>

**트리/힙**
https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html#google_vignette <br>
https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html <br>
