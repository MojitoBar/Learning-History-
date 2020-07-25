### 문제
* **카카오톡 게임별의 하반기 신규 서비스로 다트 게임을 출시하기로 했다. <br/>다트 게임은 다트판에 다트를 세 차례 던져 그 점수의 합계로 실력을 겨루는 게임으로, 모두가 간단히 즐길 수 있다.<br/> 갓 입사한 무지는 코딩 실력을 인정받아 게임의 핵심 부분인 점수 계산 로직을 맡게 되었다. 다트 게임의 점수 계산 로직은 아래와 같다.**
<br/><br/>
1. 다트 게임은 총 3번의 기회로 구성된다.

2. 각 기회마다 얻을 수 있는 점수는 0점에서 10점까지이다.

3. 점수와 함께 Single(S), Double(D), Triple(T) 영역이 존재하고 각 영역 당첨 시 점수에서 1제곱, 2제곱, 3제곱 (점수1 , 점수2 , 점수3 )으로 계산된다.

4. 옵션으로 스타상`*`, 아차상`#`이 존재하며 스타상`*` 당첨 시 해당 점수와 바로 전에 얻은 점수를 각 2배로 만든다. 아차상`#` 당첨 시 해당 점수는 마이너스된다.

5. 스타상`*`은 첫 번째 기회에서도 나올 수 있다. 이 경우 첫 번째 스타상`*`의 점수만 2배가 된다.

6. 스타상`*`의 효과는 다른 스타상`*`의 효과와 중첩될 수 있다. 이 경우 중첩된 스타상`*` 점수는 4배가 된다.

7. 스타상`*`의 효과는 아차상`#`의 효과와 중첩될 수 있다. 이 경우 중첩된 아차상`#`의 점수는 -2배가 된다.

8. Single`S`, Double`D`, Triple`T`은 점수마다 하나씩 존재한다.

9. 스타상`*`, 아차상`#`은 점수마다 둘 중 하나만 존재할 수 있으며, 존재하지 않을 수도 있다.

0~10의 정수와 문자 `S`, `D`, `T`, `*`, `#`로 구성된 문자열이 입력될 시 총점수를 반환하는 함수를 작성하라.

##### 문제 해결 순서
1. 입력받은 다트결과 문자열 길이만큼 반복문을 돈다.
2. 한 글자씩 끊어서 pick에 저장한다. </br>(**1차 삽질** 여기서 카카오 코딩테스트라는 무게감 때문인지 너무 어렵게 생각해서 정규식과 토크나이저를 사용하려 했다.<br/>근데 이러면 점수가 10점이 나오게 됐을 때, 즉 2자리 점수를 체크하기가 너무 복잡해졌다.<br/>물론 어떻게든 할 수 있었겠지만 `substring`이라는 더 쉬운 방법을 생각해냄.)
3. 각 점수, 보너스, 옵션을 step1, step2, step3으로 구분해 step1에선 점수만, step2에선 SDT만, step3에선 `#*`만 검사하게끔 나눈다.
4. step2에서 만약 pick이 "0"이라면 해당 라운드의 점수가 10점이라는 뜻이므로 score[n]을 10으로 초기화 해준다.
5. 스타상`*`이 나왔을 경우 해당 라운드가 1라운드가 아니라면 이전 라운드 점수도 2배를 해줘야 하기 때문에 29번줄에 조건문을 추가한다.
6. 만약 step3에서 옵션이 없을 경우 다음 라운드로 넘어갔다는 뜻이므로 38번줄에서 i--를 통해 순서를 맞춰준다.

```java
import java.util.StringTokenizer;
class Solution {
    public int solution(String dartResult) {
        int result = 0;
        int score[] = new int[3];
        int n = 0;
        int step = 1;
        for(int i = 0; i < dartResult.length(); i++){
            String pick = dartResult.substring(i,i+1);
            if(step == 1){
                score[n] = Integer.parseInt(pick);
                step++;
            }
            else if(step == 2){
                if(pick.equals("0")){
                    score[n] = 10;
                    step--;
                }
                else if(pick.equals("D")){
                    score[n] = score[n] * score[n];
                }
                else if(pick.equals("T")){
                    score[n] = score[n] * score[n] * score[n];
                }
                step++;
            }
            else if(step == 3){
                if(pick.equals("*")){
                    if(n >= 1){
                        score[n-1] *= 2;
                    }
                    score[n] *= 2;
                }
                else if(pick.equals("#")){
                    score[n] *= -1;
                }
                else{
                    i--;
                }
                n++;
                step = 1;
            }
        }
        result = score[0] + score[1] + score[2];
        return result;
    }
}
```

---
[참고자료 kakao Tech](https://tech.kakao.com/2017/09/27/kakao-blind-recruitment-round-1/)<br/>
[참고자료 프로그래머스](https://programmers.co.kr/)<br/>
