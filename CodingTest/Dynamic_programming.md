# 동적 프로그래밍(DP) (Dynamic Programming)
<img src="https://media.vlpt.us/images/chelsea/post/627c053e-8a71-48e7-b0b2-7b8d327963a2/%E1%84%8C%E1%85%A2%E1%84%80%E1%85%B1%E1%84%91%E1%85%B5%E1%84%87%E1%85%A9.gif" width="350"/>

- 위 같은 상황에서 이미 계산된 함수가 반복적으로 실행되는 것을 확인할 수 있다.
- 동적 프로그래밍은 위와 같은 상황에서 처음 진행되는 연산은 그 값을 저장하고, 다음번에 진행되는 똑같은 연산은 그 값을 불러오는 알고리즘이다.
- 정해진 코드나 방식이 있는게 아니라 상황에 맞는 <b>점화식</b>을 구하는 것이 키 포인트이다.
- 또한 연산의 값을 저장할 배열을 상항 염두해주어야 하고, 이를 메모이제이션(Memoization)이라 한다.

## 구현 방식
- 동적 프로그래밍의 구현방식은 크게 top-down, bottom-up으로 나뉜다.<br/>
- top-down은 보통 재귀함수로 구현하며, 원하는 값을 구하기 위해 그 이전의 값, 그 이전의 값, ... 와 같이 위에서 아래로 내려가는 방식이다.<br/>
- bottom-up은 보통 반복문으로 구현하며, 0번쨰부터 원하는 값까지 순차적으로 구해나가는, 아래에서 위로 올라가는 방식이다.

## 관련 알고리즘 문제
- [백준 9095번](https://www.acmicpc.net/problem/9095)
- [백준 14495번](https://www.acmicpc.net/problem/14495)
- [백준 1890번](https://www.acmicpc.net/problem/1890)
- [백준 2579번](https://www.acmicpc.net/problem/2579)
- [백준 1003번](https://www.acmicpc.net/problem/1003)
- [백준 9084번](https://www.acmicpc.net/problem/9084)
- [백준 11726번](https://www.acmicpc.net/problem/11726)
- [백준 12865번](https://www.acmicpc.net/problem/12865)
- [백준 1149번](https://www.acmicpc.net/problem/1149)
- [백준 1932번](https://www.acmicpc.net/problem/1932)
---
