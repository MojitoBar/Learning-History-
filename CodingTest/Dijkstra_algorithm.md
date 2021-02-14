# 다익스트라 알고리즘 (Dijkstra Algorithm)
- 기본적으로 최단거리 탐색 알고리즘이다.
<img src="https://t1.daumcdn.net/cfile/tistory/2279E23A5718AF4409" width="250"/>

- 위 그림에서 노드 1에서 노드 3으로 가는 최단거리는 노드 4를 거쳐서 가는 비용 4이다.

### 예제 코드 (백준 1753)
```Java
import java.io.*;
import java.util.*;

class Node implements Comparable<Node>{
    int end, weight;

    public Node(int end, int weight){
        this.end = end;
        this.weight = weight;
    }

    @Override
    public int compareTo(Node o) {
        return weight - o.weight;
    }
}

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int INF = 100_000_000;
    static int v,e,k;
    // 모든 정점을 저장할 배열을 List로 만드는데, List에는 배열 i번째와 연결된 모든 노드들이 저장된다.
    static List<Node>[] list;
    // 시작 노드를 기준으로 다른 모든 노드까지의 최소 비용 배열
    static int[] dist;


    public static void main(String[] args) throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        v = Integer.parseInt(st.nextToken());
        e = Integer.parseInt(st.nextToken());
        k = Integer.parseInt(br.readLine());
        list = new ArrayList[v + 1];
        dist = new int[v + 1];

        Arrays.fill(dist, INF);

        for(int i = 1; i <= v; i++){
            list[i] = new ArrayList<>();
        }
        // 리스트에 그래프 정보를 초기화
        for(int i = 0 ; i < e; i++){
            st = new StringTokenizer(br.readLine());
            int start = Integer.parseInt(st.nextToken());
            int end = Integer.parseInt(st.nextToken());
            int weight = Integer.parseInt(st.nextToken());
            // start에서 end로 가는 weight 가중치
            list[start].add(new Node(end, weight));
        }

        StringBuilder sb = new StringBuilder();
        // 다익스트라 알고리즘
        dijkstra(k);
        // 출력 부분
        for(int i = 1; i <= v; i++){
            if(dist[i] == INF) sb.append("INF\n");
            else sb.append(dist[i] + "\n");
        }

        bw.write(sb.toString());
        bw.close();
        br.close();
    }

    private static void dijkstra(int start){
       // 우선순위 큐 선언
       PriorityQueue<Node> queue = new PriorityQueue<>();
       // 노드 방문 체크 변수 선언
       boolean[] check = new boolean[v + 1];
       // 우선순위 큐에 탐색을 시작할 노드를 삽입
       queue.add(new Node(start, 0));
       // 최소비용 배열 시작번째 초기화
       dist[start] = 0;
        
       // 큐가 비어있지 않다면 
       while(!queue.isEmpty()){
           // 큐에서 뺀 노드를 현재 노드에 저장
           Node curNode = queue.poll();
           // 현재 노드의 번째를 저장
           int cur = curNode.end;
           // 현재 노드를 방문했으면 패스, 방문하지 않았으면 최소비용 검사
           if(check[cur] == true) continue;
           check[cur] = true;
           // 현재 노드와 연결된 모든 노드를 돌아가며 수행
           for(Node node : list[cur]){
               // 만약 최소비용 배열에 저장된 값(시작 노드에서부터 연결된 노드까지)이 현재 노드에서부터 연결된 노드까지의 값보다 크다면
               // 맨 위의 그림을 예로들면 노드 1(시작노드)에서부터 노드 3(연결된 노드)까지의 값이 노드 4(현재 노드)에서부터 노드 3(연결된 노드)의 값보다 크다면
               // 6 > 3 + 1
               if(dist[node.end] > dist[cur] + node.weight){
                   // 최소비용 배열의 [연결된 노드] 번째의 값을 교체
                   dist[node.end] = dist[cur] + node.weight;
                   // 큐에는 연결된 노드를 추가
                   queue.add(new Node(node.end, dist[node.end]));
               }
           }
       }
    }
}
```
- 인접 행렬을 사용하게 되면 메모리 초과가 날 수 있으니, 인접 리스트를 권장한다.
- 정점값과 시작 정점부터 해당 정점까지의 가중치를 저장하기 위해 Node를 재정의 한다.
- PriorityQueue를 사용하기위해 Node의 정렬 기준을 가중치로 한다.
- 시작 노드를 기준으로 모든 노드를 방문하며 가중치를 최단 거리로 교체해주는 것이 키포인트이다.

## 관련 알고리즘 문제
- [백준 1753번](https://www.acmicpc.net/problem/1753)
- [백준 13549번](https://www.acmicpc.net/problem/13549)
---
[동빈나의 다익스트라 알고리즘](https://m.blog.naver.com/ndb796/221234424646)<br/>
[dragonh의 다익스트라 알고리즘](https://dragon-h.tistory.com/20)
