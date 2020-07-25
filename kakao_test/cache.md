### 문제
* **지도개발팀에서 근무하는 제이지는 지도에서 도시 이름을 검색하면 해당 도시와 관련된 맛집 게시물들을 데이터베이스에서 읽어 보여주는 서비스를 개발하고 있다.<br/> 이 프로그램의 테스팅 업무를 담당하고 있는 어피치는 서비스를 오픈하기 전 각 로직에 대한 성능 측정을 수행하였는데, 제이지가 작성한 부분 중 데이터베이스에서 게시물을 가져오는 부분의 실행시간이 너무 오래 걸린다는 것을 알게 되었다.<br/> 어피치는 제이지에게 해당 로직을 개선하라고 닦달하기 시작하였고, 제이지는 DB 캐시를 적용하여 성능 개선을 시도하고 있지만 캐시 크기를 얼마로 해야 효율적인지 몰라 난감한 상황이다.<br/> 어피치에게 시달리는 제이지를 도와, DB 캐시를 적용할 때 캐시 크기에 따른 실행시간 측정 프로그램을 작성하시오.**
<br/><br/>
1. 캐시 크기`cacheSize`와 도시이름 배열`cities`을 입력받는다.

2. `cacheSize`는 정수이며, 범위는 `0 ≦ cacheSize ≦ 30` 이다.

3. `cities`는 도시 이름으로 이뤄진 문자열 배열로, 최대 도시 수는 100,000개이다.

4. 각 도시 이름은 공백, 숫자, 특수문자 등이 없는 영문자로 구성되며, 대소문자 구분을 하지 않는다. 도시 이름은 최대 20자로 이루어져 있다.

##### 문제 해결 순서
1. (**1차 삽질** `LRU`라는 캐시 교체 알고리즘을 사용해야 하는데 생전 처음보는 알고리즘이었다.<br/>알아본 결과 자료구조 Queue와 비슷한데 캐시안에 원하는 값이 있어도 최근에 사용된게 아니면 다시 맨 앞으로 가지고 와야하는 듯 하다.)<br/>
(**2차 삽질** 처음엔 직접 Queue를 구현했다. 몇 개의 테스트 케이스는 통과하는데, 일부 테스트 케이스를 통과하지 못했다.<br/> 이것 때문에 많은 시간을 날렸는데 알고보니 최근에 사용된 캐시가 아니면 다시 맨 앞으로 가지고 오는 과정을 빠트린 것이었다.)
(**3차 삽질** 모든 케이스를 통과하기 위해 코드를 짜다보니 너무 길어지고 복잡하고 더럽고 보기 싫은 코드가 되었다..<br/>이게 정말 난이도 하 문제가 맞나..? 고민하던 찰나 `LinkedList`가 문뜩 떠올랐다.)
`LinkedList`


```java
import java.util.LinkedList;
class Solution {
    public int solution(int cacheSize, String[] cities) {
        LinkedList<String> cache = new LinkedList<String>();
        int answer = 0;
        
        for(int i = 0; i < cities.length; i++){
            String city = cities[i].toUpperCase();
            
            if(cache.contains(city)){
                cache.remove(city);
                cache.add(city);
                answer += 1;
            }
            else{
                if(cacheSize > 0){
                    if(cache.size() == cacheSize){
                        cache.removeFirst();
                    }
                    cache.add(city);
                }
                answer += 5;
            }
        }
        return answer;
    }   
}
```

---
[참고자료 kakao Tech](https://tech.kakao.com/2017/09/27/kakao-blind-recruitment-round-1/)<br/>
[참고자료 프로그래머스](https://programmers.co.kr/)<br/>
