# 백트래킹 (Back Tracking)
- 백트래킹은 유망있는 (해에 가까운) 자식만을 탐색하는 알고리즘이다.
- 유명한 예로 N-Queens 문제가 있다.
<img src="https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F993E383B5C95A65521" width="250"/>

- N * N 체스판에 N 개의 퀸을 서로 잡히지 않게 끔 배치하는 경우의 수를 구하는 문제이다.
- 기본적으로 한 횡에는 하나의 퀸만 놓는다고 전제한다. (당연하다. 한 횡에 2개의 퀸이 올 수 없으니 처음부터 배제하고 시작하는것.)
- 다음 횡에는 (1, 0) ~ (1, N)까지 퀸을 놓으면서 해당 자리가 유망한지 검사한다. (해당 자리가 유망하지 않다면 3번째, 4번째... N번째 퀸이 어디 위치하든 해를 찾을 수 없다.)
- 해당 자리가 유망하다면 열이 하나 증가하고, 위 행위를 반복한다.

``` Java
import java.util.Scanner;

public class Main {
    public static int[] arr;
    public static int N;
    public static int count = 0;
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        N = in.nextInt();
        arr = new int[N];
        nQueen(0);
        System.out.println(count);
    }

    public static void nQueen(int depth) {
        // 깊이가 N이면 경우의 수 + 1
        if (depth == N) {
            count++;
            return;
        }
        // N만큼 반복하며 (depth, i)가 유망한지 검사
        for (int i = 0; i < N; i++) {
            arr[depth] = i;
            // 유망하다면 다음 depth로 이동
            if (Possibility(depth)) {
                nQueen(depth + 1);
            }
        }

    }
    public static boolean Possibility(int col) {
        // 지금까지 저장된 퀸들과 현재 퀸의 좌표 검사
        for (int i = 0; i < col; i++) {
            // 퀸이 같은 행에 존재할 경우
            if (arr[col] == arr[i]) {
                return false;
            }
            // 퀸이 대각선에 존재할 경우
            else if (Math.abs(col - i) == Math.abs(arr[col] - arr[i])) {
                return false;
            }
        }
        return true;
    }
}
```
- 백트래킹에서의 포인트는 Promising을 어떻게 체크하냐에 있다.

## 관련 알고리즘 문제
- [백준 9663번](https://www.acmicpc.net/problem/9663)
- [백준 15649번](https://www.acmicpc.net/problem/15649)
---
[뚜벅이 강군의 백트래킹](https://idea-sketch.tistory.com/29)
[주니온TV의 백트래킹 & N-Queens](https://www.youtube.com/watch?v=HRwFgtiqHH0)
