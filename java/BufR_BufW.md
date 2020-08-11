# BufferedReader 클래스
### 개요
- BufferedReader는 버퍼를 이용해서 읽는 클래스이다.
- 일반적으로 사용하는 Scanner 보다 효율이 좋다.
- Buffer는 데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 임시 메모리 영역이다.
### 사용법
```java
try{
  BufferedReader br = new BufferedReader(new InputStreamReader(System.in));    
  // readLine() 매서드 리턴값은 String이어서 숫자 입력시 형변환
  int N = Integer.parseInt(br.readLine());
  // String은 그냥 입력받음
  String s = bf.readLine();
} catch(IOException e){
  e.printStackTrace();
  System.out.println(e.getMessage());
}
```
- `readLine()`은 리턴값이 String이기 때문에 다른 자료형을 쓰려면 형변환 꼭 해주기.
- 예외처리를 꼭 해줘야한다. 입력이 버퍼크기를 벗어날수도 있기 때문에. (직접 크기를 지정해줄수도 있지만, 자바 api에는 디폴트 크기도 충분하다고 되어있다.)
- Scanner와는 다르게 엔터만 입력의 경계로 생각해서 따로 가공이 필요할 수도 있다. (StringTokenizer.nextToken, String.split을 활용)

### 주요 메소드
- read() : 한 글자만 읽어 정수형으로 반환. ('1'을 입력한다고 해서 정수 '1'이 아닌 문자 '1'의 ASCII코드 '49'를 반환)
- readLine() : 한 줄을 읽어 String으로 반환

### 개요
- BufferedWriter는 버퍼를 이용해서 출력하는 클래스이다.
- 일반적으로 사용하는 `System.out.print()` 보다 효율이 좋다.
- Buffer는 데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 임시 메모리 영역이다.
### 사용법
```java
BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
//출력할 문자열
String s = "abcdefg";
//출력
bw.write(s+"\n");
//남아있는 데이터를 모두 출력시킴
bw.flush();
//스트림을 닫음
bw.close();
```
- 버퍼를 이용하기 때문에 `flush()`와 `close()`를 써줘야한다.

### 주요 메소드
- close() : 출력 스트림을 닫음. (닫기전에 스트림이 비워져 있어야 함.)
- flush() : 남아있는 데이터를 모두 출력시켜 버퍼 스트림을 비움.
- newLine() : 문자열 줄바꿈.
- write(String s, int offset, int length) : 문자열 s를 offset 위치부터 length 길이만큼을 출력.

### 비고
- 맨날 `System.out.print`, `Scanner` 쓰다가 알고리즘 문제 푸는데 대부분이 버퍼스트림을 쓰는 것을 보고 한번 공부해봄.
- 확실히 효율이 좋긴한데 문자열을 입력받을 때 한번 가공해야하는게 귀찮긴 함.

---
[참고자료(JAVA API DOCUMENT)](https://docs.oracle.com/javase/7/docs/api/)<br/>
[참고자료(jhnyang)](https://jhnyang.tistory.com/92)<br/>
[참고자료(Machine-Geon)](https://machine-geon.tistory.com/79)
