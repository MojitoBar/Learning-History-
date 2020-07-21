# Scanner 클래스
### 개요
- 읽은 바이트를 **문자, 정수, 실수, 문자열 등 다양한 타입으로 변환**하여 리턴하는 클래스
- Scanner는 입력되는 키 값을 공백으로 구분되는 토큰 단위로 읽는다. (\t, \r, \n, ' ')
### 사용법
```java
import java.util.Scanner;    //import Scanner
Scanner scan = new Scanner(System.in);    //init Scanner
```
- System.in을 사용하여 키보드 입력 값을 읽고 원하는 타입으로 변환하여 리턴한다.
### 주요 메소드
- next() : 다음 토큰을 문자열로 리턴
- nextInt() : 다음 토큰을 int 타입으로 리턴
- nextLine() : '\n'을 포함하는 한 라인을 읽고 '\n'을 버린 나머지만 리턴
- hasNext() : 현재 입력된 토큰이 있으면 true, 아니면 새로운 입력이 들어올 때까지 무한정 기다려서, 새로운 입력이 들어오면 그때 true리턴. ctrl+z 키가 입력되면 입력 끝이므로 false 리턴
- close() : Scanner의 사용 종료
### 비고
- 스캐너는 소스코드에 하나만 사용하는 것이 이상적이다.
- close 메소드를 사용하게 되면 System.in 스트림도 함께 닫힌다.
- 웬만하면 close 메소드로 Scanner를 닫는 것이 이상적이다.

---
[참고자료(mine-it-record)](https://mine-it-record.tistory.com/103)<br/>
[참고자료(okky)](https://okky.kr/article/401102)
