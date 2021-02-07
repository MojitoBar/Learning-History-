# 너비 우선 탐색 (Breadth First Search)
- 너비 우선 탐색은 그래프를 너비를 우선순위로 탐색하는 알고리즘이다.
- 일반적으로 Queue를 사용하여 구현한다.
<img src="https://victorqi.gitbooks.io/swift-algorithm/content/Images/AnimatedExample.gif" width="250"/>

``` Java
// b 정점을 기준으로 한 탐색
public static void bfs(int b) {
    Queue<Integer> queue = new LinkedList<>();
    queue.add(b);
    // 방문한 정점임을 체크
    visit[b] = true;
    while (!queue.isEmpty()) {
        b = queue.poll();
        System.out.print(b + " ");
        for (int i = 1; i < n + 1; i++) {
            // 간선으로 연결되었으며 아직 방문하지 않은 정점
            if (map[b][i] == 1 & !visit[i]) {
                queue.offer(i);
                visit[i] = true;
            }
        }
    }
}
```

## 관련 알고리즘 문제
- [백준 1260번](https://www.acmicpc.net/problem/1260)
- [백준 2178번](https://www.acmicpc.net/problem/2178)
- [백준 2667번](https://www.acmicpc.net/problem/2667)
- [백준 2606번](https://www.acmicpc.net/problem/2606)
---
[엔지니어대한민국의 bfs와 dfs](https://www.youtube.com/watch?v=_hxFgg7TLZQ)
