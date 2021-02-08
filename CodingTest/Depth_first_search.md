# 깊이 우선 탐색 (Depth First Search)
- 깊이 우선 탐색은 그래프의 깊이를 우선순위로 탐색하는 알고리즘이다.
- 일반적으로 Stack과 재귀함수를 통해 구현한다.
- 아래에선 재귀함수를 사용한 dfs중에서도 인접행렬을 통해 구현한 코드이다.
<img src="https://media.vlpt.us/images/gillog/post/c2645862-6e8d-4b05-be8c-2e34f7737f83/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f372f37662f44657074682d46697273742d5365617263682e676966.gif" width="250"/>

``` Java
// i 정점을 기준으로 한 탐색
public static void dfs(int i){
    visit[i] = true;   // 함수 호출 시, visit 했음을 표시
    System.out.print(i+ " ");
    
    for(int j = 1; j < nV+1; j++){
        if(ad[i][j] == 1 && visit[j] == false){  // j를 방문하지 않았으면 j를 방문한다.
            dfs(j);
        }
    }
}
```

## 관련 알고리즘 문제
- [백준 1012번](https://www.acmicpc.net/problem/1012)
- [백준 11724번](https://www.acmicpc.net/problem/11724)
---
[엔지니어대한민국의 bfs와 dfs](https://www.youtube.com/watch?v=_hxFgg7TLZQ)
