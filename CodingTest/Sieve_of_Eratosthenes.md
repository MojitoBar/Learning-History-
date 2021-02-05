# 에라토스테네스의 체 (Sieve of Eratosthenes)
- 에라토스테네스의 체는 n보다 작은 모든 소수를 구하는 알고리즘이다.
<img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/Sieve_of_Eratosthenes_animation.gif" width="250"/>

``` Java
static String Sieve_of_Eratosthenes(int N) {
    String result = "";

    boolean prime[] = new boolean[N + 1];
    // 소수는 false
    // 1은 소수가 아니므로 제외
    prime[0] = prime[1] = true;

    for (int i = 2; i * i <= N; i++) {
        // prime[i]가 소수라면
        if (!prime[i]) {
            // prime[j] 소수가 아닌 표시
            for (int j = i * i; j <= N; j += i)
                prime[j] = true;
        }
    }

    // 소수 출력
    for (int i = 1; i <= N; i++) {
        if (!prime[i]) {
            result += (i + " ");
        }
    }
    return result;
}
```

## 관련 알고리즘 문제
- [백준 2960번](https://www.acmicpc.net/problem/2960)
---
[수공쌤의 에라토스테네스의 체](https://www.youtube.com/watch?v=sV3-jnfaW2E)
