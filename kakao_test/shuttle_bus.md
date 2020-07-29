### 문제
* **카카오에서는 무료 셔틀버스를 운행하기 때문에 판교역에서 편하게 사무실로 올 수 있다. 카카오의 직원은 서로를 '크루'라고 부르는데, 아침마다 많은 크루들이 이 셔틀을 이용하여 출근한다.<br/>이 문제에서는 편의를 위해 셔틀은 다음과 같은 규칙으로 운행한다고 가정하자.<br/>셔틀은 09:00부터 총 n회 t분 간격으로 역에 도착하며, 하나의 셔틀에는 최대 m명의 승객이 탈 수 있다.<br/>셔틀은 도착했을 때 도착한 순간에 대기열에 선 크루까지 포함해서 대기 순서대로 태우고 바로 출발한다. 예를 들어 09:00에 도착한 셔틀은 자리가 있다면 09:00에 줄을 선 크루도 탈 수 있다.<br/>일찍 나와서 셔틀을 기다리는 것이 귀찮았던 콘은, 일주일간의 집요한 관찰 끝에 어떤 크루가 몇 시에 셔틀 대기열에 도착하는지 알아냈다. 콘이 셔틀을 타고 사무실로 갈 수 있는 도착 시각 중 제일 늦은 시각을 구하여라.<br/>단, 콘은 게으르기 때문에 같은 시각에 도착한 크루 중 대기열에서 제일 뒤에 선다. 또한, 모든 크루는 잠을 자야 하므로 23:59에 집에 돌아간다. 따라서 어떤 크루도 다음날 셔틀을 타는 일은 없다.<br/>**

##### 문제 해결 순서

```java
import java.util.Arrays;
class Solution {
    public String solution(int n, int t, int m, String[] timetable) {
        String answer = "";
        
        int start = 540;
        int[] interval = new int[n];
        int[] last = new int[m];
        int[] convert_time = new int[timetable.length];
        int convert_answer = 0;
        
        // 타임테이블을 분으로 바꾸기
        for(int i = 0; i < convert_time.length; i++){
            int hour = Integer.parseInt(timetable[i].substring(0, 2));
            int minute = Integer.parseInt(timetable[i].substring(3, 5));
            convert_time[i] = hour * 60 + minute;
        }
        // 타임테이블 정렬
        Arrays.sort(convert_time);
        
        // 버스시간을 저장
        for(int i = 0; i < n; i++){
            interval[i] = start + (i*t);         
        }
        
        // 막차타는 사람들 last에 저장
        int j = 0;
        for(int i = 0; i < convert_time.length; i++){
          // 배차가 하나라면
          if(n <= 1 && j < m){
            // 배차시간보다 빨리 온 타임테이블을 last에 저장
            if(interval[0] > convert_time[i]){
              last[j] = convert_time[i];
              j++;
            }
          }
            // 배차가 여러개라면
          else if (n > 1 && j < m){
            // 막차 전 배차시간보다 같거나 큰 타임테이블을 last에 저장
            if(interval[n - 2] <= convert_time[i]){
              last[j] = convert_time[i];
              j++;
            }
          }
        }
        
        // 막차에 자리가 있을 때
        if(j < m){
          convert_answer = interval[n - 1];
        }
        // 막차에 자리가 없을 때
        if(j == m){
          convert_answer = last[j - 1] - 1;
        }
        // 기다리는 사람이 없으면
        if(j == 0){
          convert_answer = interval[n - 1];
        }
        
        // 분을 다시 시간 00:00 형식으로 바꾸기
        String hour = Integer.toString(convert_answer / 60);
        String minute = Integer.toString(convert_answer % 60);
        
        if(hour.length() < 2){
            answer += "0" + hour + ":";
        }
        else{
            answer += hour + ":";
        }
        if(minute.length() < 2){
          answer += "0" + minute;
        }
        else{
          answer += minute;
        }
        return answer;
    }
}
```
---
* 2020-07-29 1차 실패... 일부 예제에서만 안되는데 잘 모르겠다.
---
[참고자료 kakao Tech](https://tech.kakao.com/2017/09/27/kakao-blind-recruitment-round-1/)<br/>
[참고자료 프로그래머스](https://programmers.co.kr/)<br/>
[참고자료 코딩팩토리](https://coding-factory.tistory.com/552)
