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

- **노드 3:** `1->4->3`의 비용($1+3=4$)이 기존 비용($5$)보다 작으므로 갱신.
- **노드 5:** `1->4->5`의 비용($1+1=2$)이 기존 비용($\infty$)보다 작으므로 갱신.

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

- **노드 3:** `1->4->5->3`의 비용($2+1=3$)이 현재 비용($4$)보다 작으므로 갱신.
- **노드 6:** `1->4->5->6`의 비용($2+2=4$)이 현재 비용($\infty$)보다 작으므로 갱신.

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

# 크루스칼 알고리즘

가장 적은 비용으로 모든 노드를 연결하는 방법을 찾아내는 알고리즘으로 <br>
즉, MST를 찾는 알고리즘이다.

크루스칼 알고리즘은 그래프 내의 **모든 간선(Edge)**을 가중치(비용) 기준으로 오름차순 정렬하고, 가장 작은 간선부터 하나씩 선택한다.

## 특징

1. $O(m log m)$ time. (정렬)
2. $G’ = (V(G), T)$ 에 대해 DFS를 수행하여 판단 (각 edge 를 추가할 때 마다 최대 $O(n+m)$ time).
   총 $O(m log n) + O(m(n+m)) = O(m^2)$ time.

하지만 union-find 자료구조로 시간 복잡도를 줄일 수 있다. -> $O(E \log E)$

## 예시

각 step 마다 T 에 추가해도 cycle 이 생기지 않는 edge들 중
cost 가 가장 작은 edge 를 T(선택된 edge의 집합) 에 추가하고, 이 과정을 반복한다.

아래와 같은 그래프를 예시로 크루스칼 알고리즘을 사용하여 MST를 구하면

<img width="331" height="410" alt="화면 캡처 2026-01-05 143324" src="https://github.com/user-attachments/assets/04fd8a2d-32fb-42bc-b483-e4f5ba2b6a95" />

먼저, edge들을 cost가 높은 순서인 오름차순으로 정렬하여 준다.

| edge | 7-1 | 7-4 | 1-5 | 5-3 | 4-2 | 4-1 | 6-3 | 5-6 | 2-5 | 1-2 | 7-5 |
| :--: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| cost | 12  | 13  | 17  | 20  | 24  | 28  | 37  | 45  | 62  | 67  | 73  |

$T = { ... }$

<img width="600" height="600" alt="goodnotes-screenshot-1767591289516" src="https://github.com/user-attachments/assets/eb72a21b-f596-4e32-9913-5ba462cdea45" />

비용이 가장 적은 간선인 7-1을 선택한다. <br>

$T = { (7,1) }$

<img width="600" height="600" alt="goodnotes-screenshot-1767591366806" src="https://github.com/user-attachments/assets/fa6469e2-fe86-4427-b383-536b1c731458" />

$T$에 존재하지 않은 간선들 중 cycle이 발생하지 않고 비용이 최소인 간선인 7-4를 선택하여준다. <br>

$T = { (7,1), (7,4) }$

(최소 비용 간선 && acyclic) 조건을 준수하며 모든 노드가 연결될 때 까지 계속 진행하여준다.

<img width="600" height="600" alt="goodnotes-screenshot-1767591447688" src="https://github.com/user-attachments/assets/5861cf1d-d24a-4709-8ef4-6210e4fcfb2a" />
<img width="600" height="600" alt="goodnotes-screenshot-1767591565053" src="https://github.com/user-attachments/assets/7dd7202d-a49b-4c97-ad4d-5576c8c9fbe4" />
<img width="600" height="600" alt="goodnotes-screenshot-1767591651559" src="https://github.com/user-attachments/assets/ec32a402-62ff-4230-8449-97a66b8bbc20" />

### union-find 적용

하지만 위와 같은 방식으로 진행하면 시간 복잡도가 $O(m log n) + O(m(n+m)) = O(m^2)$ 이 된다. <br>
이를 개선하기 위해선 union-find라는 자료구조를 사용하면 된다.

https://velog.io/@xowls000/Union-find-Data-Structure-Disjoint-Set#kruskals-algorithm-using-uion-find

# 프림 알고리즘

크루스칼과 다르게 정점 위주로 S에 속한 vertex를 하나씩 늘려가면서 cut property 를 만족시키도록 edge를 골라 나가면서 MST를 찾는 알고리즘이다.

## 특징

- 시작점(노드)가 정해져있다.
- 트리가 중간에 끊어지지 않고 하나의 덩어리로 점점 커진다.
- Priority Queue(우선순위 큐)를 사용한다.

## 예시

크루스칼에서 사용한 것과 동일한 그래프를 프림 알고리즘을 사용하여 MST를 구해보면

<img width="1000" height="1220" alt="goodnotes-screenshot-1767598543604" src="https://github.com/user-attachments/assets/e5dd48e6-2a4f-48a1-a1d4-942465b03600" />

시작 정점을 7로 하고, 정점과 연결된 간선들 중 최소비용을 선택하여 확장하고, cycle 생성을 주의하면 된다.

<img width="600" height="600" alt="goodnotes-screenshot-1767598599431" src="https://github.com/user-attachments/assets/cfae9bad-fc94-4d86-835b-a52e3ca7e8f4" />

<img width="600" height="600" alt="goodnotes-screenshot-1767598626853" src="https://github.com/user-attachments/assets/666240b3-af3d-4bba-8788-10546b283645" />

<img width="600" height="600" alt="goodnotes-screenshot-1767598662812" src="https://github.com/user-attachments/assets/dbcc553a-6c82-4dd0-ad10-40af408f10f8" />

<img width="600" height="600" alt="goodnotes-screenshot-1767598689519" src="https://github.com/user-attachments/assets/1d7cbfbd-6d28-45e1-9f05-4d1550a830c4" />

<img width="600" height="600" alt="goodnotes-screenshot-1767598716350" src="https://github.com/user-attachments/assets/3edfc6ad-8c89-4639-8520-e13c954635ce" />

# 위상 정렬

위상 정렬은 방향 비순환 그래프(DAG, Directed Acyclic Graph)에서 모든 방향 간선 $u \to v$에 대해 정점 $u$가 $v$보다 먼저 오도록 하는 선형 순서이다. 예위상 정렬은 방향 비순환 그래프(DAG, Directed A

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

## 크루스칼 - 프림 알고리즘

https://m.blog.naver.com/ndb796/221230994142 <br>
https://ongveloper.tistory.com/376

## 위상 정렬

https://www.geeksforgeeks.org/dsa/topological-sorting/ <br>
https://www.youtube.com/watch?v=Th-gLZUrd04 <br>
https://www.youtube.com/watch?v=qzfeVeajuyc
