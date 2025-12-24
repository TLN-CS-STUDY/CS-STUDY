# Binary Tree

각 노드가 최대 2개의 자식노드를 가지는 트리 자료구조

## Tree traversal

트리를 순회한다는 것은 이진 트리에 속하는 모든 노드를 한 번씩 방문하여 노드가 가지고 있는 데이터를 목적에 맞게 처리하는 것을 의미한다. <br>
순회 방식에 따라 결과값이 다르기 때문에 각 순회 방식을 알아야한다. <br>

DFS, BFS는 알고리즘 part에서 다룰 예정이기 때문에 전위/중위/후위만 다룬다.

### Preorder traversal (전위 순회)

루트 → 왼쪽 → 오른쪽

<img width="500" height="410" alt="image" src="https://github.com/user-attachments/assets/0e0d66bf-b873-48c7-8e7e-36c57369fb75" />

### Inorder traversal (중위 순회)

왼쪽 → 루트 → 오른쪽

<img width="500" height="410" alt="image" src="https://github.com/user-attachments/assets/78c93697-b11f-4505-9505-8518c0f3cc5f" />

### Postorder traversal (후위 순회)

왼쪽 → 오른쪽 → 루트

<img width="500" height="410" alt="image" src="https://github.com/user-attachments/assets/bcf9c449-9bc1-42a4-8496-2c2daa6953ed" />

# Binary Search Tree (BST)

데이터를 정렬된 형태 (부모보다 작으면 왼쪽 자식, 크면 오른쪽 자식)로 저장하여 효율적인 탐색, 삽입, 삭제가 가능하게 설계된 트리 구조이다.

**Time Complexity**:
|Operation|avg case time complexity|worst case time complexity|
|:---:|:---:|:---:|
|Search <br> Insertion <br> Deletion|$O(logn)$|$O(n)$|

**worst case time complex:**
- 이진 탐색 트리가 한쪽으로 편향된 불균형 상태로, 이 경우 배열과 다를바 없어져 최악의 경우가 되고 이를 보완하기 위해 balanced BST가 존재한다. <br>

<img width="300" height="221" alt="image" src="https://github.com/user-attachments/assets/68c4731b-5b58-4c4d-b46b-88a9671a4fae" />


# AVL Tree

<img width="400" height="430" alt="image" src="https://github.com/user-attachments/assets/01870ab6-b8ca-48c0-8c7d-f20c5e1e38d7" />


불균형을 방지하기 위해 높이($h$)를 balance factor로 사용하여 rebalnce를 진행하는 AVL 트리로 불균형을 막을 수 있다.

## Feature

- 왼쪽, 오른쪽 서브 트리의 높이 차이가 최대 1 이다.
- 어떤 시점에서 높이 차이가 1보다 커지면 회전(rotation)을 통해 균형을 잡아 높이 차이를 줄인다.
- AVL 트리는 높이를 logN으로 유지하기 때문에 삽입, 검색, 삭제의 시간 복잡도는 O(logN)

### Advantages

- RB Tree와 비교해 보았을 때 height가 더 낮게 유지되고 이로 인해 serach에서 빠른 속도를 가진다.

### Disadvantages

- strict balance로 인해 RB Tree보다 실제 사용이 적다.

### Applications

- 삽입과 삭제가 빈번하게 일어나지 않지만 serach가 자주 일어나는 상황에서 사용 된다.

**Time Complexity**:
|Operation|avg / worst case time complexity|
|:---:|:---:|
|Search <br> Insertion <br> Deletion|$O(logn)$|

## Rotation

AVL Tree에서는 BF의 값이 ${-1, 0, 1}$이 아닌 경우 불균형으로 간주하고 회전을 통해 균형을 맞춥니다. <br>

> $Balance Factor (k) = height (left(k)) - height(right(k))$ <br>

- BF가 1이면 왼쪽 서브트리가 오른쪽 서브트리보다 높이가 한단계 높다는 것을 의미
- BF가 0이면 왼쪽 서브트리와 오른쪽 서브트리의 높이가 같다는 것을 의미
- BF가 -1이면 왼쪽 서브트리가 오른쪽 서브트리보다 높이가 한단계 낮다는 것을 의미

불균형은 LL/RR/LR/RL case로 나뉘며, 각 상황마다 rotation 방향을 달리하여 트리의 균형을 맞춥니다.

# RB Tree

<img width="207" height="138" alt="image" src="https://github.com/user-attachments/assets/502c5ce1-b56c-4626-8e37-9b34e7dbaf14" />

노드에 Red와 Black이라는 특성을 부여하고 아래의 규칙들을 준수하게 만들어 불균형을 해결하는 트리이다.

## Feature

- 루트는 블랙이다
- 모든 리프는 블랙이다
- 노드가 레드이면 그 노드의 자식은 반드시 블랙이다
- 루트 노드에서 임의의 리프 노드에 이르는 경로에서 만나는 블랙 노드의 수는 모두 같다

### Advantages

- AVL Tree만큼 strict balance하지 않아서, search, insertion, and deletion에서 efficient하다.

### Disadvantages

- AVL Tree에 비해 구현이 어렵다.
- small overhead가 every insertion and deletion operation에서 발생한다.

### Applications

- map, set같은 자료구조에 사용되고, file system에도 사용된다.
- in-memory database에서도 사용된다.

## Recoloring & Rotation

불균형이 발생하는 case는 LL//RR/LR/RL Case가 동일하게 존재하지만, recoloring을 먼저 시도하고 uncle node에 따라 rotation을 진행합니다. <br>

- Recoloring: Uncle node(부모의 형제)도 Red라면, 색상만 변경하여 해결합니다.
- Restructuring (Rotation): 삼촌 노드가 Black이라면, Rotation을 통해 구조를 변경합니다.

_너무 case가 다양하고 많아서 생략_

# KD Tree

<img width="400" height="394" alt="image" src="https://github.com/user-attachments/assets/43db197c-6970-42ff-9d9f-c27f35c13873" />

키가 하나로 이루어진 경우 일차원 검색 트리로 다차원에서 적용이 어렵다. <br>
그래서 두 개이상의 필드로 이루어진 키를 사용 하는 경우 필드를 그대로 검색에 사용하는 다양한 트리 (이때 키는 벡터vector 값을 갖음≈공간적 특성) 중 하나인 K-Dimensional-tree를 사용한다.

## Feature
- 이진 검색트리를 확장한 것으로 k(k≥2)의필드로 이뤄지는 키를 사용
- 각 level 이 하나의 차원만을 다룸 (=각레벨에서 필드를 번갈아 가며 검색에 사용)

### Application

다차원 탐색이 필요한 분야에 사용되며, 자세한 예시는 아래 링크에 있다. <br>
https://www.quora.com/What-is-a-kd-tree-and-what-is-it-used-for

- Nearest Neighbor Search
- 다차원 검색키 값을 갖는 데이터베이스의 쿼리 (질의문)

**Time Complexity**:
|Operation|avg case time complexity|
|:---:|:---:|
|Search <br> Insertion <br> Deletion|$O(logn)$|

# Graph

- 인접 행렬
- 인접 리스트

## 무방향 그래프

<img width="335" height="258" alt="image" src="https://github.com/user-attachments/assets/9093d9ad-e3f2-444e-a8d2-3fe7dc50e11d" />

- 두 정점을 연결하는 간선에 방향이 없는 그래프로, 간선이 양방향으로 연결되어 있어 어느 방향으로든 이동할 수 있다.

## 방향 그래프

<img width="400" height="385" alt="image" src="https://github.com/user-attachments/assets/4455ae7b-f882-4c0b-bd6d-79a76a794454" />

- Edge에 방향이 존재하는 그래프로 간선$(a,b)$는 a -> b 로는 가지만, b -> a 로는 가지 않는다.

## 가중 그래프

<img width="400" height="359" alt="image" src="https://github.com/user-attachments/assets/a52ce965-af07-49a2-8dcc-8fa78e9ee5f3" />

- 그래프의 각 간선(edge)에 수치적인 값인 가중치(weight)가 할당된 그래프이다.

# 참고자료

## Binary Tree

http://www.ktword.co.kr/test/view/view.php?no=6535 <br>
[https://laurent.tistory.com/entry/자료구조-이진-트리-순회](https://laurent.tistory.com/entry/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%9D%B4%EC%A7%84-%ED%8A%B8%EB%A6%AC-%EC%88%9C%ED%9A%8C)<br>
https://skytitan.tistory.com/97

## BST

http://www.ktword.co.kr/test/view/view.php?m_temp1=6126&id=1303 <br>
https://www.cs.usfca.edu/~galles/visualization/BST.html

## AVL Tree

https://yoongrammer.tistory.com/72 <br>
https://www.geeksforgeeks.org/dsa/introduction-to-avl-tree/

## RB Tree

https://seokyoungg.tistory.com/101 <br>
[https://www.geeksforgeeks.org/dsa/applications-advantages-and-disadvantages-of-red-black-tree/
](https://www.geeksforgeeks.org/dsa/introduction-to-red-black-tree/)
## B Tree

https://code-lab1.tistory.com/217

## B+ Tree

https://8iggy.tistory.com/191

# Graph

https://youngminieo1005.tistory.com/63 <br>
https://m.blog.naver.com/oh-mms/222045842438 <br>
https://devjourney7.tistory.com/130
