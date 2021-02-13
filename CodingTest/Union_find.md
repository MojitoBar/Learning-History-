# 유니온 파인드 (Union Find)
- 여러 노드가 존재할 때 어떤 두개의 노드가 같은 집합에 있는지 확인하는 알고리즘이다. (합집합 알고리즘.)
- 일반적으로 Find(), Union() 두 개의 함수가 존재한다.
<img src="https://disj11.github.io/assets/images/union-find-forest.png" width="250"/>

- 위 그림에는 3개의 집합이 존재한다.
- 예를 들어 노드 1, 노드 2를 연결하는 함수가 Union(), 노드 1의 부모를 찾는 함수가 Find()이다.

### Find 함수 구현
``` Java
int find(int x){
  if (x==parent[x]){
    return x;
  }
  else {
    return find[parent[x]];
  }
}
```
- 그림에서 노드 2와 3을 연결한다면 노드 3의 부모는 2로 바뀐다.
- 하지만 노드 4의 부모는 여전히 노드 3이기 때문에 노드 4의 부모를 찾을때 재귀함수를 통해 노드 3과 연결된 노드 2까지 접근해야한다.

### Union 함수 구현
```Java
void union(int x,int y){
  x = find(x);
  y = find(y);
  if (x!=y)
    parent[y] = x;
}
```
- 두 노드의 부모를 구해 서로 같지 않다면 연결할 노드의 부모에 연결될 노드의 값을 넣는다.

## 관련 알고리즘 문제
- [백준 1717번](https://www.acmicpc.net/problem/1717)
- [백준 10216번](https://www.acmicpc.net/problem/10216)
---
[동빈나의 유니온 파인드](https://www.youtube.com/watch?v=AMByrd53PHM&t=275s)<br/>
[ssung.k의 유니온 파인드](https://ssungkang.tistory.com/entry/Algorithm-%EC%9C%A0%EB%8B%88%EC%98%A8-%ED%8C%8C%EC%9D%B8%EB%93%9CUnion-Find)
