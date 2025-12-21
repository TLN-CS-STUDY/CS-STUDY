# Binary Tree

각 노드가 최대 2개의 자식노드를 가지는 것

## 이진트리의 종류

- 포화 이진트리
    - 모든 노드의 자식이 2인 (꽉찬) 이진 트리

## 이진트리의 순회

이진 트리를 순회한다는 것은 이진 트리에 속하는 모든 노드를 한 번씩 방문하여 노드가 가지고 있는 데이터를 목적에 맞게 처리하는 것을 의미한다. <br>
순회 방식에 따라 결과값이 다르기 때문에 각 순회 방식을 알아야한다.

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
- 이진 탐색 트리가 한쪽으로 편향된 불균형 상태로, 이 경우 배열과 다를바 없어져 최악의 경우가 되고 <br> 이를 보완하기 위해 balanced BST가 존재한다.


# AVL Tree

<img width="400" height="430" alt="image" src="https://github.com/user-attachments/assets/01870ab6-b8ca-48c0-8c7d-f20c5e1e38d7" />


불균형을 방지하기 위해 높이를 balance factor로 사용하여 rebalnce를 진행하는 AVL 트리를 사용한다.

## 특징

- 왼쪽, 오른쪽 서브 트리의 높이 차이가 최대 1 이다.
- 어떤 시점에서 높이 차이가 1보다 커지면 회전(rotation)을 통해 균형을 잡아 높이 차이를 줄인다.
- AVL 트리는 높이를 logN으로 유지하기 때문에 삽입, 검색, 삭제의 시간 복잡도는 O(logN)

> $Balance Factor (k) = height (left(k)) - height(right(k))$

- BF가 1이면 왼쪽 서브트리가 오른쪽 서브트리보다 높이가 한단계 높다는 것을 의미
- BF가 0이면 왼쪽 서브트리와 오른쪽 서브트리의 높이가 같다는 것을 의미
- BF가 -1이면 왼쪽 서브트리가 오른쪽 서브트리보다 높이가 한단계 낮다는 것을 의미

**Time Complexity**:
|Operation|avg / worst case time complexity|
|:---:|:---:|
|Search <br> Insertion <br> Deletion|$O(logn)$|

# RB Tree

<img width="207" height="138" alt="image" src="https://github.com/user-attachments/assets/502c5ce1-b56c-4626-8e37-9b34e7dbaf14" />

노드에 Red와 Black이라는 특성을 부여하여, 불균형을 해결하는 트리

## 특징

- 루트는 블랙이다
- 모든 리프는 블랙이다
- 노드가 레드이면 그 노드의 자식은 반드시 블랙이다
- 루트 노드에서 임의의 리프 노드에 이르는 경로에서 만나는 블랙 노드의 수는 모두 같다

# KD Tree

<img width="400" height="394" alt="image" src="https://github.com/user-attachments/assets/43db197c-6970-42ff-9d9f-c27f35c13873" />

키가 하나로 이루어진 경우 일차원 검색 트리로 다차원에서 적용이 어렵다. <br>
그래서 두 개이상의 필드로 이루어진 키를 사용 하는 경우 필드를 그대로 검색에 사용하는 다양한 트리 (이때 키는 벡터vector 값을 갖음≈공간적 특성) 중 하나인 KD-Tree를 사용한다.

## 특징
- 이진 검색트리를 확장한 것으로 k(k≥2)의필드로 이뤄지는 키를 사용
- 각 level 이 하나의 차원만을 다룸 (=각레벨에서 필드를 번갈아 가며 검색에 사용)

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

http://www.ktword.co.kr/test/view/view.php?m_temp1=6126&id=1303

## AVL Tree

https://yoongrammer.tistory.com/72

## RB Tree

https://seokyoungg.tistory.com/101

## B Tree

https://code-lab1.tistory.com/217

## B+ Tree

https://8iggy.tistory.com/191

# Graph

https://youngminieo1005.tistory.com/63 <br>
https://m.blog.naver.com/oh-mms/222045842438 <br>
https://devjourney7.tistory.com/130
