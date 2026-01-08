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
## 2.1. Kruskal

## 2.2. Prim

# 3. 정렬 및 탐색(Sort & Search)
## 3.1. 위상 정렬(Topological Sort)

## 3.2. DFS(깊이 우선 탐색)

## 3.3. BFS(너비 우선 탐색)


***
# 참고자료
## Dijkstra
https://cobi-98.tistory.com/46
https://doitforus.tistory.com/162
https://hongl.tistory.com/48#google_vignette
## 크루스칼

## 프림

## 위상 정렬

## DFS

## BFS
