### 문제
* **네오는 평소 프로도가 비상금을 숨겨놓는 장소를 알려줄 비밀지도를 손에 넣었다. <br/>그런데 이 비밀지도는 숫자로 암호화되어 있어 위치를 확인하기 위해서는 암호를 해독해야 한다. <br/>다행히 지도 암호를 해독할 방법을 적어놓은 메모도 함께 발견했다.**
<br/><br/>
1. 지도는 한 변의 길이가 n인 정사각형 배열 형태로, 각 칸은 “공백”(“ “) 또는 “벽”(“#”) 두 종류로 이루어져 있다.

2. 전체 지도는 두 장의 지도를 겹쳐서 얻을 수 있다. 각각 “지도 1”과 “지도 2”라고 하자. 지도 1 또는 지도 2 중 어느 하나라도 벽인 부분은 전체 지도에서도 벽이다. 지도 1과 지도 2에서 모두 공백인 부분은 전체 지도에서도 공백이다.

3. “지도 1”과 “지도 2”는 각각 정수 배열로 암호화되어 있다.

4. 암호화된 배열은 지도의 각 가로줄에서 벽 부분을 1, 공백 부분을 0으로 부호화했을 때 얻어지는 이진수에 해당하는 값의 배열이다.

![예시이미지](http://t1.kakaocdn.net/welcome2018/secret8.png)


##### 문제 해결 순서
1. 입력 받는 arr1, arr2 두 배열을 비트연산자 or을 이용해 합친다.
2. 합친 10진수를 `Integer.toBinaryString`을 통해 2진수로 바꾼 후 새로운 배열에 저장한다.
3. 바뀐 2진수의 길이를 `String.format("%5s", 2진수)`을 통해 맞춰준다. 
<br/>(**1차 고비** 저장된 result는 문자열이기 때문에 %s를 사용해야하는데 자꾸 %d를 씀.)
<br/>(**2차 고비** 문자열보다 숫자가 크면 공백으로 채우게 되는데 그걸 자꾸 다시 0으로 바꾸려고 애씀. 결국 0을 공백으로 바꿀것이기 때문에 무시해도 됐음.)
4. replace()를 통해 1 -> #으로, 0 -> 공백으로 바꿔주어 return 해준다.


```java
class Solution {
    public String[] solution(int n, int[] arr1, int[] arr2) {
        String[] result = new String[n];
        for(int i = 0; i < n; i++){
            result[i] = Integer.toBinaryString(arr1[i] | arr2[i]);
        }
        
        for(int i = 0; i < n; i++){
            result[i] = String.format("%" + n + "s", result[i]);
            result[i] = result[i].replace("1", "#");
            result[i] = result[i].replace("0", " ");
        }
                                   
        return result;
    }
}
```

---
[참고자료 kakao Tech](https://tech.kakao.com/2017/09/27/kakao-blind-recruitment-round-1/)<br/>
[참고자료 프로그래머스](https://programmers.co.kr/)<br/>
[참고자료 micropai](https://micropai.tistory.com/48)
