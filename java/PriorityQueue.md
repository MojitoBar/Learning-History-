# PriorityQueue 클래스
### 개요
- 우선순위 큐(PriorityQueue)는 들어간 순서에 상관없이 일정한 규칙에 따라 우선순위를 정하고, 우선순위가 가장 높은 데이터가 가장 먼저 나오게 된다.
- 기본적으로 숫자는 낮은 것이 우선순위고, `Comparator`클래스나 `Comparable` 인터페이스를 이용하면 오름차순으로 사용할 수 있다.
### 사용법
- 내림차순 (기본 값)
```java
PriorityQueue<Integer> priorityQueue = new PriorityQueue<>();

priorityQueue.add(4); //offer(); 메소드를 사용해도 동일하게 추가됩니다.
priorityQueue.add(3);
priorityQueue.add(2);
priorityQueue.add(1);

Integer poll = priorityQueue.poll;
System.out.println(poll); //출력결과 1
```
- 오름차순 (`Collections.reverseOrder()`을 통해 오름차순으로 변경)
```java
//우선순위를 높은 숫자위주로 변경
PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(Collections.reverseOrder());

priorityQueue.add(1); //offer(); 메소드를 사용해도 동일하게 추가됩니다.
priorityQueue.add(2);
priorityQueue.add(3);
priorityQueue.add(4);

Integer poll = priorityQueue.
System.out.println(poll); //출력결과 4
```
### 주요 메소드
- add(e), offer(e) : 지정된 원소를 우선순위 큐에 삽입
- poll() : 큐의 헤드 값을 큐에서 제거하고 그 값을 리턴, 없으면 null을 리턴
- peek() : 큐의 헤드값을 리턴, 없으면 null을 리턴
- contain(o) : 큐에 지정된 요소가 포함되어 있으면 true를 리턴. 지정된 요소가 포함되어 있지 않으면 false를 리턴
### 비고
- 정렬을 마음대로 사용하려면 다른 클래스나 인터페이스의 이해가 필요하다.
- 이 클래스 덕분에 JAVA API 문서를 처음으로 찾아보게 되었다.
- add()와 offer()은 똑같이 큐에 원소를 삽입하는 함수이지만, 다른 인터페이스에서 제공한다는 차이가 있다. 그 외에는 똑같은 듯.

---
[참고자료(JAVA API DOCUMENT)](https://docs.oracle.com/javase/7/docs/api/)<br/>
[참고자료(siyoon210)](https://siyoon210.tistory.com/117)
[참고자료(stackoverflow)](https://stackoverflow.com/questions/15591431/difference-between-offer-and-add-in-priority-queue-in-java)
