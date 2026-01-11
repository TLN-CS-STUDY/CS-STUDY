# 1. 최단 경로 알고리즘(Shorteest Path)
## 1.1. Dijkstra
- 음의 가중치(음의 간선, 음의 값)가 없는 그래프의 한 노드에서 각 모든 노드까지의 최단거리르 구하는 알고리즘
### 1.1.1. 작동 예시
1. 초기화
<img width="641" height="661" alt="Image" src="https://github.com/user-attachments/assets/d92a8e12-bf97-47e7-a96b-12386b72bf81" />

2. 출발 노드 설정
<img width="641" height="741" alt="Image" src="https://github.com/user-attachments/assets/5ea7a548-a379-4e16-9cf2-5f76c669adfb" />

3. 방문하지 않은 노드 중 최단 거리 노드 선택
<img width="641" height="741" alt="Image" src="https://github.com/user-attachments/assets/69326cad-8d91-4446-be95-27211ea4fd61" />

4. 반복
<img width="641" height="741" alt="Image" src="https://github.com/user-attachments/assets/3f7aba52-753e-4748-ab98-9836e6af0c74" />
<img width="641" height="741" alt="Image" src="https://github.com/user-attachments/assets/7c1042f6-f158-41ff-95a2-6565aa2ac89e" />
<img width="641" height="741" alt="Image" src="https://github.com/user-attachments/assets/53674b9d-9d04-4e94-8f26-44a0f042879a" />
<img width="641" height="741" alt="Image" src="https://github.com/user-attachments/assets/e817e13f-f19d-4802-94f8-6d9b5169e023" />
<img width="641" height="741" alt="Image" src="https://github.com/user-attachments/assets/3ea44e0e-19d2-4ac1-82e1-b66833a6c3e5" />

6. 결과
<img width="641" height="741" alt="Image" src="https://github.com/user-attachments/assets/fc212f91-d26a-43fd-aa5f-fccc6c0edb7e" />

### 1.1.3. 구현
- 순차탐색 방식
```
public class DijkstraSequential {
    static int n, m; // 노드 개수, 간선 개수
    static final int INF = (int) 1e9;
    static int[][] graph; // 인접 행렬
    static int[] d; // 최단 거리 테이블
    static boolean[] visited; // 방문 처리용

    public static int getNextNode() {
        int minDistance = INF;
        int index = 0;
        for (int i = 1; i <= n; i++) {
            if (d[i] < minDistance && !visited[i]) {
                minDistance = d[i];
                index = i;
            }
        }
        return index;
    }

    public static void dijkstra(int start) {
        d[start] = 0;
        visited[start] = true;

        // 시작 노드와 연결된 노드들 초기화
        for (int i = 1; i <= n; i++) {
            if (graph[start][i] != INF) d[i] = graph[start][i];
        }

        // 시작 노드를 제외한 n-1개 노드에 대해 반복
        for (int i = 0; i < n - 1; i++) {
            int now = getNextNode(); // 현재 가장 짧은 노드 선택 (순차 탐색)
            visited[now] = true;

            for (int j = 1; j <= n; j++) {
                // 현재 노드를 거쳐서 j로 가는 거리가 더 짧으면 갱신
                if (d[now] + graph[now][j] < d[j]) {
                    d[j] = d[now] + graph[now][j];
                }
            }
        }
    }
}
```

- 우선순위 큐 방식
```
import java.util.*;

// 우선순위 큐에서 정렬 기준을 잡기 위해 Comparable 구현
class Node implements Comparable<Node> {
    int index, distance;

    Node(int index, int distance) {
        this.index = index;
        this.distance = distance;
    }

    @Override
    public int compareTo(Node other) {
        return this.distance - other.distance; // 거리 짧은 순 (오름차순)
    }
}

public class DijkstraPriorityQueue {
    static int n, m;
    static final int INF = (int) 1e9;
    static ArrayList<ArrayList<Node>> graph = new ArrayList<>(); // 인접 리스트
    static int[] d;

    public static void dijkstra(int start) {
        PriorityQueue<Node> pq = new PriorityQueue<>();
        pq.offer(new Node(start, 0));
        d[start] = 0;

        while (!pq.isEmpty()) {
            Node node = pq.poll();
            int dist = node.distance;
            int now = node.index;

            // 핵심 최적화: 큐에서 꺼낸 거리가 이미 저장된 거리보다 크면 무시
            if (d[now] < dist) continue;

            // 현재 노드와 연결된 노드들 확인
            for (Node neighbor : graph.get(now)) {
                int cost = d[now] + neighbor.distance;
                if (cost < d[neighbor.index]) {
                    d[neighbor.index] = cost;
                    pq.offer(new Node(neighbor.index, cost));
                }
            }
        }
    }
}
```

# 2. 최소 신장 트리(Minimum Spanning Tree)
- Spanning Tree
    - 연결 그래프의 부분 그래프이며, 그래프에서 모든 정점을 포함
    - 정점 간 서로 연결이 되어 있어야 함
    - 사이클이 존재하지 않는 그래프
    - 연결 그래프에서 신장트리는 1개가 아닌 다수일 수 있음
<img width="705" height="777" src="https://github.com/user-attachments/assets/408738b8-2ee6-4a13-98ad-c2d3976981db" />

- Minimum Spanning Tree
    - Spanning Tree 중 가중치의 합이 최소가 되는 신장 트리
    
## 2.1. Kruskal
### 2.1.1. 작동 원리
1. 가중치를 오름차순 정렬
<img width="761" height="238" src="https://github.com/user-attachments/assets/f8a974b2-9fb8-4b1c-8775-b636d7f5f2d2" />

2. 정렬된 순서대로 간선 확인
<img width="757" height="244" alt="Image" src="https://github.com/user-attachments/assets/f7b90680-03f2-4cc7-9219-1b12fc7084c6" />

<img width="744" height="237" alt="Image" src="https://github.com/user-attachments/assets/f213d027-fdf1-43af-8fc9-b6987bf37f72" />

3. 사이클 검사
<img width="745" height="246" alt="Image" src="https://github.com/user-attachments/assets/8dd811bb-67b6-43f1-92d8-ea5f1be12951" />

4. 반복
<img width="760" height="244" alt="Image" src="https://github.com/user-attachments/assets/0a681f61-617a-4e00-bdf5-c1109f8c4f66" />

### 2.1.2. 구현
```
// 간선 정보를 담는 클래스
class Edge implements Comparable<Edge> {
    int nodeA, nodeB, distance;

    Edge(int nodeA, int nodeB, int distance) {
        this.nodeA = nodeA;
        this.nodeB = nodeB;
        this.distance = distance;
    }

    @Override
    public int compareTo(Edge other) {
        return Integer.compare(this.distance, other.distance); // 가중치 기준 오름차순
    }
}

public class KruskalExample {
    static int v, e; // 노드와 간선 개수
    static int[] parent = new int[100001];
    static ArrayList<Edge> edges = new ArrayList<>();

    // 특정 원소가 속한 집합의 루트 노드 찾기 (Path Compression 최적화)
    public static int findParent(int x) {
        if (x == parent[x]) return x;
        return parent[x] = findParent(parent[x]);
    }

    // 두 원소가 속한 집합을 합치기
    public static void unionParent(int a, int b) {
        a = findParent(a);
        b = findParent(b);
        if (a < b) parent[b] = a;
        else parent[a] = b;
    }

    public static void main(String[] args) {
        // 1. 부모 테이블 초기화 (자기 자신을 부모로 설정)
        for (int i = 1; i <= v; i++) parent[i] = i;

        // 2. 모든 간선을 가중치에 따라 오름차순 정렬
        Collections.sort(edges);

        int totalCost = 0;
        for (Edge edge : edges) {
            // 3. 사이클이 발생하지 않는 경우에만 집합에 포함
            if (findParent(edge.nodeA) != findParent(edge.nodeB)) {
                unionParent(edge.nodeA, edge.nodeB);
                totalCost += edge.distance;
            }
        }
        System.out.println("최소 신장 트리 비용: " + totalCost);
    }
}
```

### 2.1.3. Union-Find
- 서로소 집합을 표현하는 자료구조
- Union
    - 서로 다른 두 집합을 병합 연산
- Find
    - 집합 원소가 어떤 집합에 속해있는지 찾는 연산

## 2.2. Prim
- 시작 정점에서 저점을 추가해가며 단계적으로 트리를 확장하는 기법
### 2.2.1. 작동 원리
<img width="290" height="265" alt="Image" src="https://github.com/user-attachments/assets/de76b4bc-4a34-428e-8b4a-b479bc467321" />

1. 시작 정점 선택
<img width="290" height="265" alt="Image" src="https://github.com/user-attachments/assets/a82bcc0a-071f-4cef-bdb3-98118702c8c4" />

2. 간선 탐색
    - 아직 방문하지 않은 노드로 가는 가중치가 작은 간선 찾기
<img width="290" height="265" alt="Image" src="https://github.com/user-attachments/assets/90b24110-92b9-4cad-aa83-0a8f21bc1973" />

3. 정점 추가
4. 반복

<img width="290" height="265" alt="Image" src="https://github.com/user-attachments/assets/5a0b8678-4633-4047-a744-7d55faecc221" />
<img width="290" height="265" alt="Image" src="https://github.com/user-attachments/assets/802a474f-e59a-47cb-9358-fc11c5d5feb0" />
<img width="290" height="265" alt="Image" src="https://github.com/user-attachments/assets/6e2f9a80-7348-41d8-aa53-d988ecc99b69" />
<img width="290" height="265" alt="Image" src="https://github.com/user-attachments/assets/151187fe-c037-4002-81ce-154f1e75699d" />

### 2.2.2. 구현
```
class Edge implements Comparable<Edge> {
    int to, weight;

    Edge(int to, int weight) {
        this.to = to;
        this.weight = weight;
    }

    @Override
    public int compareTo(Edge other) {
        return Integer.compare(this.weight, other.weight);
    }
}

public class PrimExample {
    static ArrayList<ArrayList<Edge>> graph = new ArrayList<>();
    static boolean[] visited;

    public static int prim(int start, int v) {
        PriorityQueue<Edge> pq = new PriorityQueue<>();
        pq.offer(new Edge(start, 0)); // 시작 노드 (가중치 0으로 시작)
        
        int totalWeight = 0;
        int count = 0; // 연결된 노드 수

        while (!pq.isEmpty()) {
            Edge edge = pq.poll();
            int now = edge.to;
            int weight = edge.weight;

            // 이미 방문한 노드라면 건너뜀
            if (visited[now]) continue;

            // 방문 처리 및 결과 합산
            visited[now] = true;
            totalWeight += weight;
            count++;

            // 현재 노드와 연결된 인접 노드들을 큐에 삽입
            for (Edge next : graph.get(now)) {
                if (!visited[next.to]) {
                    pq.offer(next);
                }
            }
            
            // 모든 노드를 다 찾았다면 종료 (최적화)
            if (count == v) break;
        }
        return totalWeight;
    }
}
```

# 3. 정렬 및 탐색(Sort & Search)
## 3.1. 위상 정렬(Topological Sort)
- 비순환 방향 그래프(Directed Acyclic Graph)
<img width="1071" height="431" alt="Image" src="https://github.com/user-attachments/assets/36dfde13-6ed3-447b-842a-21b1aa260329" />

### 3.1.1. 동작 원리
1. 진입차수가 0인 모든 노드를 큐에 넣는다
2. 큐가 빌 때까지 반복
3. 결과

### 3.1.2. 구현
```
public class TopologicalSortExample {
    static int v, e; // 노드와 간선 개수
    static int[] indegree; // 모든 노드에 대한 진입차수 배열
    static ArrayList<ArrayList<Integer>> graph = new ArrayList<>();

    public static void topologicalSort() {
        ArrayList<Integer> result = new ArrayList<>(); // 알고리즘 수행 결과를 담을 리스트
        Queue<Integer> q = new LinkedList<>();

        // 1. 처음 시작할 때 진입차수가 0인 노드를 큐에 삽입
        for (int i = 1; i <= v; i++) {
            if (indegree[i] == 0) {
                q.offer(i);
            }
        }

        while (!q.isEmpty()) {
            // 2. 큐에서 원소 꺼내기
            int now = q.poll();
            result.add(now);

            // 3. 해당 원소와 연결된 노드들의 진입차수에서 1 빼기
            for (int next : graph.get(now)) {
                indegree[next]--;
                // 4. 새롭게 진입차수가 0이 되는 노드를 큐에 삽입
                if (indegree[next] == 0) {
                    q.offer(next);
                }
            }
        }

        // 결과 출력 (만약 result의 사이즈가 v보다 작다면 사이클이 발생한 것)
        for (int node : result) {
            System.out.print(node + " ");
        }
    }
}
```
## 3.2. DFS(깊이 우선 탐색)
- 루트 노드(혹은 임의의 노드)에서 시작해서 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법
### 3.2.1. 동작 원리
1. 시작 노드 방문
2. 인접 노드 탐색
3. 막히면 되돌아가기
4. 반복
<img width="1974" height="1529" alt="Image" src="https://github.com/user-attachments/assets/b7f67467-fe4f-4997-98ac-e90d668ad34a" />

### 3.2.2. 구현
```
public class DFSExample {
    static boolean[] visited = new boolean[9]; // 방문 처리 배열
    static ArrayList<ArrayList<Integer>> graph = new ArrayList<>();

    // DFS 함수 정의
    public static void dfs(int x) {
        // 1. 현재 노드를 방문 처리
        visited[x] = true;
        System.out.print(x + " ");

        // 2. 현재 노드와 연결된 다른 노드를 재귀적으로 방문
        for (int next : graph.get(x)) {
            if (!visited[next]) {
                dfs(next);
            }
        }
    }

    public static void main(String[] args) {
        // 그래프 초기화 및 간선 연결 로직 생략
        // dfs(1); // 1번 노드부터 시작
    }
}
```
## 3.3. BFS(너비 우선 탐색)
### 3.3.1. 동작 원리
1. 시작 노드 방문
2. 인접 노드 탐색
3. 반복
<img width="1993" height="2482" alt="Image" src="https://github.com/user-attachments/assets/854f9c39-c73f-4b50-a722-a44121f8d2af" />

### 3.3.2. 구현
```
public class BFSExample {
    static boolean[] visited = new boolean[9];
    static ArrayList<ArrayList<Integer>> graph = new ArrayList<>();

    public static void bfs(int start) {
        Queue<Integer> q = new LinkedList<>();
        
        // 1. 시작 노드를 큐에 넣고 방문 처리
        q.offer(start);
        visited[start] = true;

        // 큐가 빌 때까지 반복
        while (!q.isEmpty()) {
            // 2. 큐에서 노드를 하나 꺼냄
            int x = q.poll();
            System.out.print(x + " ");

            // 3. 인접한 노드 중 방문하지 않은 노드를 모두 큐에 삽입
            for (int next : graph.get(x)) {
                if (!visited[next]) {
                    q.offer(next);
                    visited[next] = true; // 큐에 넣을 때 방문 처리 (중복 방지)
                }
            }
        }
    }
}
```

***
# 참고자료
## 최단 경로 알고리즘(Shorteest Path)
https://cobi-98.tistory.com/46
https://doitforus.tistory.com/162
https://hongl.tistory.com/48#google_vignette
## 최소 신장 트리(Minimum Spanning Tree)
https://chanhuiseok.github.io/posts/algo-33/
https://velog.io/@jxlhe46/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-MST
https://8iggy.tistory.com/159
## 정렬 및 탐색(Sort & Search)
https://velog.io/@kimdukbae/%EC%9C%84%EC%83%81-%EC%A0%95%EB%A0%AC-Topological-Sorting
https://ryu-e.tistory.com/100
https://je0ng-dev-log.tistory.com/41