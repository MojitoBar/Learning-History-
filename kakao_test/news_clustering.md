### 문제
* **여러 언론사에서 쏟아지는 뉴스, 특히 속보성 뉴스를 보면 비슷비슷한 제목의 기사가 많아 정작 필요한 기사를 찾기가 어렵다.<br/>Daum 뉴스의 개발 업무를 맡게 된 신입사원 튜브는 사용자들이 편리하게 다양한 뉴스를 찾아볼 수 있도록 문제점을 개선하는 업무를 맡게 되었다.**
<br/><br/>
1. 입력으로는 str1과 str2의 두 문자열이 들어온다. 각 문자열의 길이는 2 이상, 1,000 이하이다.

2. 입력으로 들어온 문자열은 두 글자씩 끊어서 다중집합의 원소로 만든다. 이때 영문자로 된 글자 쌍만 유효하고, 기타 공백이나 숫자, 특수 문자가 들어있는 경우는 그 글자 쌍을 버린다. 예를 들어 “ab+”가 입력으로 들어오면, “ab”만 다중집합의 원소로 삼고, “b+”는 버린다.

3. 다중집합 원소 사이를 비교할 때, 대문자와 소문자의 차이는 무시한다. “AB”와 “Ab”, “ab”는 같은 원소로 취급한다.

4. 입력으로 들어온 두 문자열의 자카드 유사도를 출력한다. 유사도 값은 0에서 1 사이의 실수이므로, 이를 다루기 쉽도록 65536을 곱한 후에 소수점 아래를 버리고 정수부만 출력한다.

##### 문제 해결 순서
1. 유사도 검사에서 대소문자를 구별하지 않기 때문에 `toUpperCase()`로 전부 대문자로 바꿔준다.
2. 반복문을 돌며 `substring()`을 통해 두 글자씩 잘라 배열에 넣는데 이때 정규식을 통해 영문자를 제외한 문자를 걸러낸다.
3. `contains()`를 통해 arr1배열에 arr2배열의 원소가 포함되어있는지 확인하고 있으면 교집합 +1
4. 두 집합(A, B)의 합집합의 크기는 A + B - 교집합을 통해 합집합과 교집합의 크기를 구한다.

```java
import java.util.*;
import java.util.regex.Pattern;
class Solution {
    public int solution(String str1, String str2) {
        int answer = 0;
        // 합집합, 교집합 변수
        int intersection = 0;
        int union = 0;
        // 두 문자열을 잘라 저장할 배열
        ArrayList<String> arr1 = new ArrayList();
        ArrayList<String> arr2 = new ArrayList();
        // 영문자를 제외한 문자들을 걸러내기위한 패턴 선언
        String p = "^[a-zA-Z]*$";
        // 입력받은 문자열 2개를 전부 대문자로 바꿈
        str1 = str1.toUpperCase();
        str2 = str2.toUpperCase();
        // substring(i - 2, i)로 2글자씩 잘라 반복문을 돌며 영문자 패턴이 true면 ArrayList에 추가.
        for(int i = 2; i <= str1.length(); i++){
          if(Pattern.matches(p, str1.substring(i - 2, i))){
            arr1.add(str1.substring(i - 2, i));
          }
        }
        // substring(i - 2, i)로 2글자씩 잘라 반복문을 돌며 영문자 패턴이 true면 ArrayList에 추가.
        for(int i = 2; i <= str2.length(); i++){
          if(Pattern.matches(p, str2.substring(i - 2, i))){
            arr2.add(str2.substring(i - 2, i));
          }
        }
        // 합집합에 두 배열의 길이를 더함
        intersection = arr1.size() + arr2.size();
        // 반복문을 돌며 arr2배열에 arr1원소가 있는지 확인, 있으면 arr2배열에서 삭제하고 교집합 +1
        for(int i = 0; i < arr1.size(); i++){
            if(arr2.contains(arr1.get(i))){
                arr2.remove(arr1.get(i));
                union++;
            }
        }
        // 집합a + 집합b - 교집합 = 합집합
        intersection -= union;
        // 자카드 유사도에서 교집합과 합집합이 0 이면 유사도는 1
        if(union == 0 && intersection == 0){
            answer = 65536;
        }
        // 교집합은 없지만 합집합이 있으면 유사도는 0
        else if(union == 0 && intersection != 0){
            answer = 0;
        }
        // 교집합 / 합집합 * 65536
        else{
          answer = (int)(((float)union / (float)intersection) * 65536);
        }
        
        return answer;
    }
}
```
---
* 난이도 (중) 문제였지만 왠지 (하) 풀때만큼 쉽게 풀림. 자카드 유사도에 대해 이번에 처음 들어봄.
---
[참고자료 kakao Tech](https://tech.kakao.com/2017/09/27/kakao-blind-recruitment-round-1/)<br/>
[참고자료 프로그래머스](https://programmers.co.kr/)<br/>
[참고자료 HIGHCODE](https://highcode.tistory.com/6)<br/>
