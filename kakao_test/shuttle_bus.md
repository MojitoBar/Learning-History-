### 문제
* **카카오에서는 무료 셔틀버스를 운행하기 때문에 판교역에서 편하게 사무실로 올 수 있다. 카카오의 직원은 서로를 '크루'라고 부르는데, 아침마다 많은 크루들이 이 셔틀을 이용하여 출근한다.<br/><br/>이 문제에서는 편의를 위해 셔틀은 다음과 같은 규칙으로 운행한다고 가정하자.<br/><br/>셔틀은 09:00부터 총 n회 t분 간격으로 역에 도착하며, 하나의 셔틀에는 최대 m명의 승객이 탈 수 있다.<br/><br/>셔틀은 도착했을 때 도착한 순간에 대기열에 선 크루까지 포함해서 대기 순서대로 태우고 바로 출발한다. 예를 들어 09:00에 도착한 셔틀은 자리가 있다면 09:00에 줄을 선 크루도 탈 수 있다.<br/><br/>일찍 나와서 셔틀을 기다리는 것이 귀찮았던 콘은, 일주일간의 집요한 관찰 끝에 어떤 크루가 몇 시에 셔틀 대기열에 도착하는지 알아냈다. 콘이 셔틀을 타고 사무실로 갈 수 있는 도착 시각 중 제일 늦은 시각을 구하여라.<br/><br/>단, 콘은 게으르기 때문에 같은 시각에 도착한 크루 중 대기열에서 제일 뒤에 선다. 또한, 모든 크루는 잠을 자야 하므로 23:59에 집에 돌아간다. 따라서 어떤 크루도 다음날 셔틀을 타는 일은 없다.<br/>**

##### 문제 해결 순서
1. `PriorityQueue`를 통해 크루가 도착하는 시간을 오름차순으로 정렬하여 저장하는 `crew`를 선언
2. `timetable`의 시간을 분 형식으로 바꾸고 `crew`에 저장
3. n이 0으로 갈 때까지 반복문을 돌며 크게 3가지 경우로 구분. 첫 차일 때, 마지막 배차버스일 때, 아닐 때
4. (첫 차) 현재 배차시간보다 일찍왔고 기다리는 크루가 있고 자리가 있다면 수용인원을 -1, `time`에 `crew.poll()` 값을 넣음
5. (막차가 아닐 때) 배차가 1 이상이고 기다리는 크루가 없다면, 첫 차에 다 탔다는 뜻. 그러면 막차를 타면 됨.
6. (막차가 아닐 때) 배차가 1 이상이고 기다리는 크루가 있다면, 버스를 다음 시간으로.
7. (막차일 때) 수용인원이 남아 있으면 막차를 타면 됨.
8. (막차일 때) 수용인원이 남아있지 않으면 마지막으로 탄 크루보다 1분 일찍 오면됨.
```java
import java.util.*;
class Solution {
    public String solution(int n, int t, int m, String[] timetable) {
        String answer = "";
        //크루가 도착하는 시간을 오름차순으로 정렬
        PriorityQueue<Integer> crew = new PriorityQueue<>();
        
        for(String table : timetable){
            //크루의 도착시간을 문자열->Integer 형태로 변환
            int time = Integer.parseInt(table.substring(0, 2)) * 60 + Integer.parseInt(table.substring(3));
            crew.add(time);
        }
        int busTime = 9 * 60;
        int last = 0;
        while(n-->0){
            //수용인원을 초기화
            int accept = m; 
            //마지막으로 탄 크루의 시간
            int time = 0;
            //기다리는 크루가 있다면
            while(!crew.isEmpty()){
                //현재 버스의 도착시간보다 일찍왔으며, 자리가 있을 때
                if(crew.peek() <= busTime && accept > 0){
                    accept--;
                    time = crew.poll();
                }
                else{
                    break;
                }
            }
            //마지막 버스가 아니면
            if(n > 0){
                //기다리는 크루가 없다면
                if(crew.isEmpty()){
                    //막차시간
                    last = busTime + ((n + 1) * t);
                    break;
                }
                //기다리는 크루가 있으면 버스 다음시간
                busTime += t;
            }
            //마지막 버스이면
            else{
                //자리가 있으면 버스 시간으로
                if(accept > 0){
                    last = busTime;
                }
                //자리가 없으면 마지막으로 탄 크루보다 1분 일찍
                else{
                    last = time - 1;
                }
                break;
            }
        }
        answer = String.format("%02d", last / 60) + ":" + String.format("%02d", last % 60);
        return answer;
    }
}
```
* 2020-07-29 1차 실패... 일부 예제에서만 안되는데 잘 모르겠다.
* 1차때 접근 방식은 막차시간을 구하고 그 시간에 탈 수 있는 인원을 구한 뒤 ... 이런 식으로 풀었는데 예외가 너무 많았다.<br/>오히려 큐를 만들어서 크루를 한명씩 빼면서 계산하는게 더 정확한듯.<br/>풀 땐 진짜 어려웠는데, 막상 풀고 보니까 딱 난이도 중 정도인것 같다.
* 차분하게 수도코드먼저 작성하는게 큰 도움을 주는듯. 그리고 자바 내장함수들을 잘 활용하는 것도 실력인게 틀림없다.
---
[참고자료 kakao Tech](https://tech.kakao.com/2017/09/27/kakao-blind-recruitment-round-1/)<br/>
[참고자료 프로그래머스](https://programmers.co.kr/)
