# 유클리드 호제 (Euclidean_algorithm)
- 유클리드 호제법은 두 수의 최대공약수를 구하는 알고리즘이다.
- a > b 일때, a와 b의 최대공약수는 b와 a%b의 최대공약수와 같다.
- 재귀함수를 이용, a%b의 값이 0일때, b가 a, b의 최대공약수.

``` Java
int gcd(int a, int b) {
  if (a % b == 0)
    return b;
  return gcd(b, a % b);
}
```

## 관련 알고리즘 문제
- [백준 2609번](https://www.acmicpc.net/problem/2609)
- [백준 1934번](https://www.acmicpc.net/problem/1934)
- [백준 9613번](https://www.acmicpc.net/problem/9613)
- [백준 1735번](https://www.acmicpc.net/problem/1735)
- [백준 1850번](https://www.acmicpc.net/problem/1850)
---
[yerin4847의 유클리드 호제법](https://velog.io/@yerin4847/W1-%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C-%ED%98%B8%EC%A0%9C%EB%B2%95)
<br/>
[수악중독의 유클리드 호제법](https://www.youtube.com/watch?v=J5Yl2kHPAY4)
