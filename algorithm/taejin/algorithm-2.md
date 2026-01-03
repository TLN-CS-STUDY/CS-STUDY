# 위상 정렬

위상 정렬은 방향 비순환 그래프(DAG, Directed Acyclic Graph)에서 모든 방향 간선 $u \to v$에 대해 정점 $u$가 $v$보다 먼저 오도록 하는 선형 순서이다.

즉, 순서가 정해져 있는 작업들을 차례대로 나열하는 것이다.

## 특징

- DAG에서만 가능: 방향성이 있고 사이클이 없는 그래프(DAG)에만 적용되며, 순환 그래프나 무방향 그래프에는 적용할 수 없다.

- 여러 개의 답 존재: 하나의 그래프에는 여러 개의 위상 정렬 결과가 존재할 수 있다.

- 의존성 순서: 일반적인 DFS/BFS 탐색과 달리, 정점 간의 선후 관계(의존성)를 지키며 나열한다.

## 예시

보통 수강신청을 예시로 많이 설명한다.

자료구조 $\to$ 알고리즘 (자료구조를 들어야 알고리즘 수강 가능) <br>
알고리즘 $\to$ 졸업프로젝트 <br>
데이터베이스 $\to$ 졸업프로젝트 <br>
이산수학 (선수 과목 없음) <br>

위 과목들을 순서대로 듣는 방법은 

1: 이산수학 $\to$ 자료구조 $\to$ 데이터베이스 $\to$ 알고리즘 $\to$ 졸업프로젝트 <br>
2: 자료구조 $\to$ 이산수학 $\to$ 알고리즘 $\to$ 데이터베이스 $\to$ 졸업프로젝트

이렇게 두 가지 방법이 있을 것이다.

즉, 순서만 맞게 정렬한다면 여러가지 답이 존재할 수 있다.

## 구현

그러면 이를 구현하기 위해서 알고리즘 적으로 생각을 해보면, 진입 차수의 유무와 큐를 사용하면 된다.

아래와 같은 DAG를 예시로 하면

<img width="500" height="500" alt="goodnotes-screenshot-1767454330682" src="https://github.com/user-attachments/assets/16c5aa0e-4fb2-4e7b-b90b-0914d4cec305" />

1. 모든 노드의 진입 차수를 계산한다.

2. 진입 차수가 0인 노드(선행 조건이 없는 작업)를 찾아서 큐에 넣는다.

3. 큐에서 노드를 하나 꺼내서 결과 리스트에 추가한다.

4. 완료된 노드와 연결된 간선를 모두 끊는다. (지운다)

5. 이때, 연결되어 있던 다음 노드들의 진입 차수를 1씩 줄인다.

6. 새롭게 진입 차수가 0이 된 노드가 있다면 큐에 넣는다.

7. 큐가 빌 때까지 반복한다.

<img width="500" height="500" alt="goodnotes-screenshot-1767454672096" src="https://github.com/user-attachments/assets/88989a59-1a56-4420-9b02-ad2e58effaec" />

<img width="500" height="500" alt="goodnotes-screenshot-1767454796268" src="https://github.com/user-attachments/assets/c2baf2e9-776f-488d-9c2a-decdaefeef0c" />

<img width="500" height="500" alt="goodnotes-screenshot-1767454925503" src="https://github.com/user-attachments/assets/a7796059-fa6a-4908-aee4-5f78a796c267" />

<img width="500" height="500" alt="goodnotes-screenshot-1767455023926" src="https://github.com/user-attachments/assets/29dbf207-903f-4bb0-9bfb-cb16c90558a5" />

<img width="500" height="500" alt="goodnotes-screenshot-1767455139972" src="https://github.com/user-attachments/assets/8e340177-ee7d-4081-ba7d-a7b30906452f" />

<img width="500" height="500" alt="goodnotes-screenshot-1767455207671" src="https://github.com/user-attachments/assets/cfb6fc85-62c6-4f99-b2da-ba180971e27a" />

a -> b -> e -> c -> d -> f -> g

시간 복잡도: $O(V + E)$ (V: 정점의 개수, E: 간선의 개수)

# 참고 자료

## 위상 정렬
https://www.geeksforgeeks.org/dsa/topological-sorting/ <br>
https://www.youtube.com/watch?v=Th-gLZUrd04 <br>
https://www.youtube.com/watch?v=qzfeVeajuyc
