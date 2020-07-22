---
ing
---

10s*10s*10s*  4 8 12
1s1s1s*    3 5 7
s*s*s*
sss*
import java.util.StringTokenizer;
class Solution {
    public int solution(String dartResult) {
        int answer = 0;
        int score[] = new int[3];
        int result[] = new int[3];
        String bonus = dartResult.replaceAll("[0-9*#]", "");
        StringTokenizer token = new StringTokenizer(dartResult, "SDT*#");
        for(int i = 0; token.hasMoreTokens(); i++){
            score[i] = Integer.parseInt(token.nextToken());
        }
        
        for(int i = 0; i < 3; i++){
            if(bonus.charAt(i) == 'S'){
                result[i] = score[i];
            }
            else if(bonus.charAt(i) == 'D'){
                result[i] = score[i] * score[i];
            }
            else if(bonus.charAt(i) == 'T'){
                result[i] = score[i] * score[i] * score[i];
            }
        }
        
        for (int i = 0; i < dartResult.length(); i++){
            if(dartResult.charAt(i) == '*' && (i >= 3 && i <= 4)){
                result[0] *= 2;
            }
            if(dartResult.charAt(i) == '*' && (i >= 6 && i <= 8)){
                result[0] *= 2;
                result[1] *= 2;
            }
            if(dartResult.charAt(i) == '*' && (i >= 9 && i <= 12)){
                result[1] *= 2;
                result[2] *= 2;
            }
            if(dartResult.charAt(i) == '#' && (i >= 3 && i <= 4)){
                result[0] *= -1;
            }
            if(dartResult.charAt(i) == '#' && (i >= 6 && i <= 8)){
                result[1] *= -1;
            }
            if(dartResult.charAt(i) == '#' && (i >= 9 && i <= 12)){
                result[2] *= -1;
            }
        }
        answer = result[0] + result[1] + result[2];
        return answer;
    }
}

1S2D*3T

SDT
123

1
4
27

