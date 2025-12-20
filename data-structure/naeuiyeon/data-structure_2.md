# 1. 이진트리(Binary Tree)
- 트리 중에서도 각 노드가 최대 2개의 자식 노드를 갖는 트리
<img width="1055" height="379" src="https://github.com/user-attachments/assets/c2c99519-b14d-4924-93b0-5652e2aae9b1" />

## 1.1. 이진트리 유형
### 1.1.1. 전 이진트리(Full Binary Tree or Strict Binary Tree)
- 모든 노드가 0개 또는 2개의 자식 노드를 갖는 트리
### 1.1.2. 완전 이진트리(Complete Binary Tree)
- 마지막 레벨을 제외하고 모든 레벨이 완전히 채워져 있는 트리
### 1.1.3. 포화 이진트리(Perfect Binary Tree)
- 모든 내부 노드가 두 개의 자식 노드를 가지며 모든 잎 노드가 동일한 깊이 또는 레벨을 갖는 트리
### 1.1.4. 균형 이진트리(Balanced Binary Tree)
- 왼쪽과 오른쪽 트리의 높이 차이가 모두 1만큼 나는 트리

***

# 2. Complete Binary Tree
<img width="640" height="226" src="https://github.com/user-attachments/assets/360d9f77-ded2-470b-a225-c6467e38a0fa" />

## 2.1. Red-Black Tree
- 균형 이진 탐색 트리(Self-balancing Binary Search Tree)의 일종
- 삽입 및 삭제 연산이 발생할 때도 트리의 균형을 유지하여 탐색, 삽입, 삭제 등의 연산을 O(log n)의 시간복잡도로 보장
- 최악의 경우(한쪽으로 치우친 트리)를 방지하기 위해 고안된 트리

<img width="683" height="603" src="https://github.com/user-attachments/assets/17cd1b48-22c2-4cef-b682-ee1d2b5cdd54" />

### 2.1.1. 특징
- 균형 유지
    - 트리의 높이가 어느 한쪽으로 지나치게 치우치지 않도록 설계되어 있으며, 최악의 경우에도 트리의 높이가 노드 수 n에 대해 2 * log(n + 1)을 넘지 않음
- 색상 규칙
    - 노드의 색상에 따라 회전 또는 색상 변경을 수행하여 트리의 규칙을 만족
- 회전 연산
    - 삽입 삭제 후 불균형이 발생할 때 회전과 색상 변화를 통해 균형 유지
### 2.1.2. 규칙
1. 노드 색상 규칙
- 각 노드는 red 또는 black
2. 루트 노드 규칙
- 루트 노드는 항상 black
3. 리프 노드 규칙
- 트리의 모든 리프 노드(NIL)는 black
4. red-red 규칙
- 두 개의 연속된 레드 노드가 존재할 수 없음
5. 경로 규칙
- 각 노드에서 NIL에 이르는 모든 경로는 같은 수의 블랙 노드를 포함해야함 => 블랙 높이 (black-height)
### 2.1.3. 연산
#### 2.1.3.1. Insert
- 삽입하는 노드의 색은 항상 red
- 삽입된 노드의 부모가 black인 경우
    - 규칙 위반이 없으므로 더 이상의 작업 x
    - 트리의 규칙을 그대로 유지한채 삽입 완료
- 삽입된 노드의 부모가 red인 경우
    - red-red 위반으로 이를 해결하기 위해 색상 변경, 회전 연산 또는 두 가지를 모두 사용
#### 2.1.3.2. Delete
- 삭제 후에는 이중 블랙 문제(Double Black)가 발생할 수 있으며, 이러한 문제가 발생하면 이를 해결하기 위해 색상 변경(Recoloring)과 회전(Restructuring)이 필요
##### * Double Black이란? 주로 블랙 노드 삭제로 인해 발생하는 문제로, 트리의 균형을 유지하기 위한 규칙을 위반하는 상태
- 삭제할 노드가 두 자식을 가지는 경우
    - 두 자식 노드를 가진 경우에서는 후계자 노드의 값을 삭제할 노드의 위치로 복사
        - 이때 후계자의 색상은 복사되지 않고, 후계자 값(혹은 Entry의 Key와 Value)만 복사
        - 이후 실제 삭제 대상의 위치는 후계자 자리가 됨
    - 후계자가 Red든 Black이든 후계자 자리에서 삭제가 이루어지며, 후계자가 Black이면 이중 블랙 문제가 발생할 수 있음
        - 후계자가 Red면, 단순히 지우기만 하면 됨
- 실제로 삭제되는 노드가 Black인 경우
    - Black 노드를 삭제하면 이중 블랙 문제 발생 가능성
        - 블랙 높이 규칙을 위반하는 상태로, 색상 변경과 회전을 통해 해결

## 2.2. AVL Tree
- 균형 이진 탐색 트리(Self-balancing Binary Search Tree)의 일종
- 트리의 높이를 항상 일정하게 유지하여 탐색, 삽입, 삭제 연산에서 O(log n)의 성능을 보장하는 자료구조
- 삽입이나 삭제 시 트리의 균형을 유지하기 위해 회전(Rotation) 연산 사용
    - 비균형 트리로 인한 성능 저하 방지

<img width="510" height="340" src="https://github.com/user-attachments/assets/f1272472-9db5-4ca5-971c-528c861133de" />

### 2.2.1. 특징
1. 균형 인수 (Height Balance Factor)
- AVL Tree에서는 각 노드에 대해 왼쪽 서브트리와 오른쪽 서브트리의 높이 차이를 균형 인수라고 함
- 균형 인수는 -1, 0, 1을 유지해야 함
    - 0 : 왼쪽과 오른쪽 서브트리의 높이가 동일함
    - 1 : 왼쪽 서브트리의 높이가 오른쪽보다 1 크다는 의미
    - -1 : 오른쪽 서브트리의 높이가 왼쪽보다 1 크다는 의미
2. 회전 연산
- 트리의 균형을 유지하지 못할 때, 회전 연산을 통해 균형을 되찾음
- 단순 회전(Single Rotation)
    - 트리가 한쪽 방향으로만 치우친 경우 사용
    - LL, RR
- 이중 회전(Double Rotation)
    - 두 방향으로 치우친 경우 사용
    - LR, RL
3. 시간 복잡도
- 탐색, 삽입, 삭제 연산 모두에서 O(log n) 성능 보장

## 2.3. B Tree
- 트리의 노트가 한방향으로 쏠리지 않도록, 노드를 삽입 및 삭제하는 경우, 규칙에 맞도록 트리를 재정렬하여 왼쪽과 오른쪽 노드의 밸런스를 항상 유지하는 트리
- 일반으로 트리 구조를 탐색하는 경우 O(log n)의 시간복잡도를 가지지만, 트리 노드의 요소가 한쪽으로 쏠리는 최악의 경우 O(N)의 시간 복잡도를 갖게 된다. 이러한 경우를 방지하기 위해 데이터베이스의 인덱스에서는 Balanced Tree를 사용
### 2.3.1. 특징
- 노드 내 여러 개의 키
- 정렬된 상태 유지
- 자식 노드의 수 k + 1
- 자가 균형
### 2.3.2. B-Tree vs B+Tree

|특징|B-Tree|B+Tree|
|---|---|---|
|데이터 저장|모든 노드에 데이터 저장 가능|리프 노드에만 실제 데이터 저장|
|연결성|리프 노드 간 연결 없음|리프 노드들이 연결 리스트로 연결된|
|탐색|중간 노드에서 탐색 종료 가능|무조건 리프 노드까지 내려가야 함|
|장점|단일 데이터 검색이 빠를 수 있음|범위검색에 매우 효과적|

## 2.4. Multidimensional Search Tree
### 2.4.1. KD-Tree
- 이진 검색 트리(BST)를 확장한 것으로, k(k >= 2)개의 필드로 이루어진 키를 다룸
- 각 레벨(Level)마다 하나의 차원(필드)만을 번갈아 가며 분기 기준으로 사용
    - 한 레벨에서는 하나의 필드만 사용
    - 총 k개의 필드를 사용하는 검색이라면, k개의 레벨을 내려가며 검색에 사용하는 필드가 일치
### 2.4.2. 구조 및 구성 방식
|구성요소|설명|예시|
|---|---|---|
|분할 축(Splitting Axis)|각 노드가 데이터를 분할하는 기준 축|X축, Y축, Z축 등 순차 반복|
|분할 값(Splitting Value)|선택된 축에서의 기준값|중위값(median) 기반 분할 선|
|노드(Node)|좌표와 관련 정보 저장|(x, y), (r, g, b), (latitude, longitude) 등|
|서브트리(Subtree)|좌/우 하위 공간 노드|분할 기준보다 작거나 큰 영역으로 재귀 구성|
### 2.4.3. 시간 복잡도
|연산|평균 시간복잡도|최악 시간복잡도|
|--|---|---|
|삽입|O(log n)|O(n)|
|삭제|O(log n)|O(n)|
|검색|O(log n)|O(n)|
|최근접 이웃 검색|O(log n)|O(n)|
### 2.4.4. 연산
#### 2.4.4.1. 삽입
1. 축 결정
- 현재 노드의 depth를 d라고 할 때, 비교할 축은 depth (mod k)로 결정됨
2. 비교 및 이동
- 추가하려는 점의 해당 축 좌표가 현재 노드의 좌표보다 작으면 왼쪽 자식으로 이동
- 크거나 같으면 오른쪽 자식으로 이동
3. 반복
- 비어있는 Leaf Node 위치에 도달할 때까지 1~2번을 반복하여 새로운 노드 삽입
#### 2.4.4.2. 삭제
1. 자식이 없는 경우 (Leaf Node)
- 그냥 삭제
2. 오른쪽 자식이 있는 경우
- N의 오른쪽 서브트리에서 i번째 축의 값이 최소인 노드(M)를 찾음
- N의 위치에 M의 데이터를 덮음
- 이제 원래 M이 있던 위치의 노드를 재귀적으로 삭제
3. 왼쪽 자식만 있는 경우
- 왼쪽 서브트리에서 i번째 축의 최소값을 찾아 올리는 것이 아니라, 최소값 노드(M)를 찾아 N의 위치로 올린 뒤, 원래의 왼쪽 서브트리 전체를 오른쪽으로 옮김
### 2.4.5. 알고리즘
- 최근접 이웃(NN) 탐색
```
public class KDTree {
    private Node root;
    private final int K = 2;

    private Node bestNode = null;
    private double bestDist = Double.MAX_VALUE;

    // 최근접 이웃 찾기 시작 함수
    public int[] findNearest(int[] target) {
        bestNode = null;
        bestDist = Double.MAX_VALUE;
        searchNearest(root, target, 0);
        return bestNode.point;
    }

    private void searchNearest(Node current, int[] target, int depth) {
        if (current == null) return;

        // 1. 현재 노드와 거리 계산
        double d = distance(current.point, target);
        if (d < bestDist) {
            bestDist = d;
            bestNode = current;
        }

        int cd = depth % K;
        Node next = (target[cd] < current.point[cd]) ? current.left : current.right;
        Node other = (target[cd] < current.point[cd]) ? current.right : current.left;

        // 2. 일단 타겟이 속한 방향으로 먼저 내려감
        searchNearest(next, target, depth + 1);

        // 3. 가지치기 (Pruning): 반대편 영역에 더 가까운 게 있을 가능성 확인
        // 타겟과 분할 평면(축) 사이의 거리가 현재 최단거리보다 작아야만 탐색
        if (Math.pow(target[cd] - current.point[cd], 2) < bestDist) {
            searchNearest(other, target, depth + 1);
        }
    }

    private double distance(int[] p1, int[] p2) {
        return Math.pow(p1[0] - p2[0], 2) + Math.pow(p1[1] - p2[1], 2);
    }
}
```


***

# 3. 그래프
- Vertex와 Edge로 이루어진 자료구조
- Vertex간의 관계를 표현하는 조직도
## 3.1. 기본 구조
|용어|설명|
|---|---|
|정점(Vertices)|그래프에서 ‘데이터’를 나타내는 개별 요소를 말합니다. 노드(Node)라고도 불립니다.|
|간선(Edge)|그래프에서 ‘정점간의 관계’를 나타내는 선입니다. 연결선이라고도 불립니다.|
|가중치(Weight)|그래프의 ‘간선(Edge)에 할당된 값’으로, 간선(Edge)의 중요도 또는 비용을 나타냅니다.|
|차수(Degree)|정점에 연결된 ‘간선(Edge)의 개수’를 말합니다. 정점의 연결성을 나타내는 지표입니다.|
|경로(Path)|그래프에서 정점들을 연결하는 ‘간선(Edge)들의 순서대로 나열한 것’을 말합니다.|
|사이클(Cycle)|그래프에서 경로의 ‘시작점과 끝점이 동일한 경우’를 말합니다. 즉, 동일한 정점을 여러 번 방문하는 경로입니다.|
|연결성(Connectedness)|그래프에서 정점들이 얼마나 잘 연결되어 있는지를 나타내는 지표입니다.|
|플레너리티(Planarity)|그래프에서 사이클이 없는 경우를 말합니다. 즉, 모든 경로가 사이클을 형성하지 않는 그래프입니다.|
|이분 그래프(Bipartiteness)|그래프의 정점들을 두 개의 그룹으로 나눌 수 있는 그래프를 말합니다. 각 그룹 내의 정점들끼리는 서로 연결되어 있지 않아야 합니다.|
## 3.2. 종류
<img width="1100" height="594" src="https://github.com/user-attachments/assets/578f40dc-c910-43fc-8274-51ab4f02e5a0" />

|그래프|유형분류|설명|
|---|---|---|
|무방향 그래프|방향의 유무|간선에 방향이 없는 그래프로 노드들이 서로 연결됩니다.|
|방향 그래프|방향의 유무|간선에 방향이 있는 그래프로 간선은 출발 노드와 도착 노드를 가리킵니다.|
|가중 그래프|가중치의 유무|간선에 가중치가 있는 그래프로 가중치는 노드 간의 관계나 거리 등을 나타냅니다.|
|연결 그래프|임의의 두 노드 연결 여부|그래프에서 모든 노드가 최소한 하나의 경로로 연결된 그래프입니다.|
|비연결 그래프|임의의 두 노드 연결 여부|그래프에서 일부 노드가 다른 노드와 연결되지 않은 그래프입니다.|
|순환 그래프|순환 여부|그래프에 사이클이 존재하는 그래프로 한 노드에서 시작하여 다시 해당 노드로 돌아올 수 있는 경로가 있는 그래프입니다.|
|비순환 그래프|순환 여부|그래프에 사이클이 존재하지 않는 그래프로 한 노드에서 시작하여 해당 노드로 돌아오는 경로가 없는 그래프입니다.|
## 3.3. 무방향 그래프(Undirected Graph)
- 간선에 '방향이 없는 그래프'로 노드들이 서로 연결
- 각각의 노드가 서로를 향하는 방향을 가리키지 않는 그래프
- 노드들이 서로 연결되어 있으며 간선은 양방향으로 표현
- 즉, '한 노드에서 다른 노드로 갈 수 있는 경로'가 존재하면 그 노드들은 무방향 그래프에서 연결되어 있다고 볼 수 있음
- 깊이 우선 탐색(DFS), 너비 우선 탐색(BFS), 최소 신장 트리(MST)
## 3.4. 방향 그래프(Directed Graph)
- 간선에 '방향이 있는 그래프'로 간선은 출발 노드와 도착 노드를 가리킴
- 각각의 노드가 서로를 향해 방향을 가리키는 그래프
- 한 노드에서 다른 노드로 갈 수 있는 경로가 있을때만 그 노드들은 방향 그래프에서 연결되어 있다고 볼 수 있음
- 깊이 우선 탐색(DFS), 너비 우선 탐색(BFS), 위상 정령(Topological Sort)

***

# 참고자료
## 이진트리
https://yoongrammer.tistory.com/69
## Complete Binary Tree
https://www.blog.data101.io/105
https://velog.io/@dankj1991/Tree-Red-Black-Tree-Part1
https://blogshine.tistory.com/102
https://velog.io/@dankj1991/Tree-AVL-Tree
https://velog.io/@qqqqld/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-AVL-%ED%8A%B8%EB%A6%AC
https://suyeonme.tistory.com/102
https://velog.io/@xowls000/Multidimensional-Search-Tree
## 그래프
https://hongcoding.tistory.com/78