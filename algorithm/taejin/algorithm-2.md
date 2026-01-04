# 다익스트라(Dijkstar) 알고리즘

**특정한 하나의 정점**에서 출발하여 **다른 모든 정점**까지의 최단 경로를 구하는 알고리즘이다.
매 단계마다 방문하지 않은 노드 중 **가장 비용이 적은 노드**를 선택(Greedy)하여 이동하며, 연결된 노드들의 최단 거리를 갱신하는 방식으로 동작한다.

## 특징

- **음의 간선 사용 불가**
   - 간선(Edge)의 가중치가 음수일 경우 사용할 수 없다. (음의 간선이 있다면 '벨만-포드' 알고리즘 사용)
   - 현실 세계의 도로 간 거리는 음수가 없으므로, 네비게이션(GPS) 등 현실 문제 해결에 적합하다.

- **거리 테이블(Distance Table) 사용**
   - 출발 노드로부터 다른 모든 노드까지의 최단 거리를 저장하는 1차원 리스트를 사용한다.
   - 이전까지 구했던 최단 거리 정보를 이용하여 새로운 거리를 계산한다.

## 예시

아래와 같은 그래프에서 다익스트라 알고리즘을 사용하여 시작 노드부터 다른 모든 노드까지의 최단 거리를 구하는 알고리즘을 실행해보자.
<img width="400" height="391" alt="image" src="https://github.com/user-attachments/assets/cd06f949-a098-429d-8f9b-a4313d46b66e" />

모든 노드의 거리를 무한대($\infty$)로, 방문 여부를 `false`로 초기화한다.

**최단 거리 테이블**
| node | 1 | 2 | 3 | 4 | 5 | 6 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| cost | $\infty$ | $\infty$ | $\infty$ | $\infty$ | $\infty$ | $\infty$ |
| isVisited | false | false | false | false | false | false |

<img width="400" height="391" alt="image" src="https://github.com/user-attachments/assets/bb9ea188-2fdb-473c-9b7c-bca219ab7d07" />

시작 노드 **1**을 선택하여 방문 처리(`true`)하고 비용을 **0**으로 갱신한다.
그리고 1과 연결된 노드(2, 3, 4)들의 거리를 갱신(Update)한다.

**최단 거리 테이블**
| node | 1 | 2 | 3 | 4 | 5 | 6 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| cost | **0** | **2** | **5** | **1** | $\infty$ | $\infty$ |
| isVisited | **true** | false | false | false | false | false |

<img width="400" height="391" alt="image" src="https://github.com/user-attachments/assets/77295e70-62cc-4839-8eaa-d7b888b059cf" />

방문하지 않은 노드 중 비용이 가장 적은 **노드 4**를 방문한다. <br>
노드 4와 연결된 노드 3, 5에 대해 거리를 계산한다.

* **노드 3:** `1->4->3`의 비용($1+3=4$)이 기존 비용($5$)보다 작으므로 갱신.
* **노드 5:** `1->4->5`의 비용($1+1=2$)이 기존 비용($\infty$)보다 작으므로 갱신.

**최단 거리 테이블**
| node | 1 | 2 | 3 | 4 | 5 | 6 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| cost | 0 | 2 | **4** | 1 | **2** | $\infty$ |
| isVisited | true | false | false | **true** | false | false |

<img width="400" height="391" alt="image" src="https://github.com/user-attachments/assets/1e8aaad9-37f5-4105-9774-a74657df0d31" />

다음으로 비용이 적은 노드는 2와 5(비용 2로 동일)이다.<br>
번호 순서상 **노드 2**를 먼저 방문한다. <br>
노드 2를 거쳐 3으로 가는 비용($2+3=5$)은 현재 비용($4$)보다 크므로 갱신하지 않는다.

**최단 거리 테이블**
| node | 1 | 2 | 3 | 4 | 5 | 6 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| cost | 0 | 2 | 4 | 1 | 2 | $\infty$ |
| isVisited | true | **true** | false | true | false | false |

<img width="400" height="391" alt="image" src="https://github.com/user-attachments/assets/1a8d96f1-2a9c-4a09-be52-2be0ae05d21b" />

그 다음 비용이 적은 **노드 5**를 방문한다.<br>
노드 5와 연결된 노드 3, 6에 대해 거리를 계산한다.

* **노드 3:** `1->4->5->3`의 비용($2+1=3$)이 현재 비용($4$)보다 작으므로 갱신.
* **노드 6:** `1->4->5->6`의 비용($2+2=4$)이 현재 비용($\infty$)보다 작으므로 갱신.

**최단 거리 테이블**
| node | 1 | 2 | 3 | 4 | 5 | 6 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| cost | 0 | 2 | **3** | 1 | 2 | **4** |
| isVisited | true | true | false | true | **true** | false |

<img width="400" height="391" alt="image" src="https://github.com/user-attachments/assets/8e3cfc1f-b83f-4b73-8bc5-fde65dae88e4" />

<img width="400" height="391" alt="image" src="https://github.com/user-attachments/assets/3ac0ce81-7ab8-4845-8e5f-1a3d0bab7ab1" />

남은 노드 중 비용이 가장 적은 **노드 3(비용 3)**을 방문 처리한다. <br>
마지막으로 **노드 6(비용 4)**을 방문 처리한다. <br>
더 이상 갱신할 경로가 없으므로 알고리즘을 종료한다.

**최종 최단 거리 테이블**
| node | 1 | 2 | 3 | 4 | 5 | 6 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| cost | 0 | 2 | 3 | 1 | 2 | 4 |
| isVisited | **true** | **true** | **true** | **true** | **true** | **true** |

<img width="400" height="391" alt="image" src="https://github.com/user-attachments/assets/900a2903-396e-4b39-a836-a7808e989d6d" />


## 구현

다익스트라 알고리즘은 BFS 를 기반으로 구현할 수 있다.

2가지로 구현할 수 있는데, 거리 테이블을 매번 탐색하는 순차 탐색 방식과 거리가 짧은 노드를 우선 탐색하는 우선순위 큐를 이용한 방식이 있다.
 
   - 순차 탐색 방식(인접 행렬 방식): $O(V^2)$
   - **우선순위 큐(Priority Queue) 방식:** $O(E \log V)$

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

## 다익스트라 알고리즘
https://www.youtube.com/watch?v=o9BnvwgPT-o <br>
https://m.blog.naver.com/ndb796/221234424646

## 위상 정렬
https://www.geeksforgeeks.org/dsa/topological-sorting/ <br>
https://www.youtube.com/watch?v=Th-gLZUrd04 <br>
https://www.youtube.com/watch?v=qzfeVeajuyc
