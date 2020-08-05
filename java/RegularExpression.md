# 정규 표현식 (Regular Expression)
### 개요
- 정규 표현식은 줄여서 정규식이라고도 하며, 영어로는 Regular Expression, 줄여서 regex, regexp라고도 한다.
- 정규 표현식은 특정한 규칙을 가진 문자열의 집합을 표현하기 위해 쓰이는 형식 언어이다.
### 사용법
##### Java 정규 표현식의 종류
- UNIX 계열의 표준 정규표현식인 POSIX의 정규 표현식
- POSIX 정규표현식에서 확장된 Perl방식의 정규표현식
- Java에서는 Perl의 방식과 유사한 방식을 선택하고 있으나, Perl 방식과 완전히 똑같은 것은 아니고, 그 차이점은 [oralcle문서](https://docs.oracle.com/javase/tutorial/essential/regex/index.html)에 수록되어 있다.

##### 정규 표현식 예제
- `java.util.regex`의 Pattern과 Matcher 클래스를 사용하여 정규 표현식을 다룰 수 있다.
* 가장 간단한 예제
```java
// 아무 문자 다음에 at문자가 오는지
final String regex = ".at$";
// 검사할 문자열
String str  = "cat";
System.out.println(str.matches(regex));
```
- `String.matches()`를 이용해 인자로 정규식을 받아 패턴이 일치하는지를 리턴한다.

* regex 라이브러리를 이용한 예제
```java
// regex 관련 라이브러리 추가
import java.util.regex.Pattern;
import java.util.regex.Matcher;
// 패턴 컴파일
Pattern p = Pattern.compile(".at");
// 패턴에 맞춰볼 문자열을 넘겨 Matcher 객체로 받는다.
Matcher m = p.matcher("cat");
// 일치하면 true, 아니면 false
System.out.println(m.matches());
```
- 이 방식의 장점은 Pattern 객체를 생성하여 compile을 한 번 실행 한다면, 그 다음 다시 사용할 때 컴파일을 하지 않아도 된다는 점.
- 패턴의 재사용이 많을 시 유용하다.

##### 패턴 기본 문법
|정규식|설명|예제|
|---|---|---|
|`.`|임의의 한 문자(필수)를 의미|`ab. (abc, abd...)`|
|`?`|바로 앞에 문자가 없거나 하나가 있음을 의미|`a?c (ac, abc, bc...)`|
|`*`|바로 앞에 문자가 없거나 하나이상 반복을 의미|`ab* (a, ab, aaa...)`|
|`+`|바로 앞에 문자가 하나이상 반복을 의미|`ab+ (ab, abb, abbb...)`|
|`^`|문자열의 시작을 의미|`^ab (abc, abcd, abcde)...`|
|`[^]`|`^`이후의 괄호안 형식을 제외함을 의미|`[^ab]cd (ecd, fcd, gcd...)`|
|`$`|문자열의 끝을 의미 합니다.|`abc$ (pupu abc, story abc...)`|
|`[0-9]`|괄호안의 숫자가 있음을 의미|`[0-9] (0, 1, 2, 3...)`|
|`[a-z]`|괄호안의 소문자 영어가 있음을 의미|`[a-z] (a, b, c, d...)`|
|`[a-zA-Z]`|괄호안의 대,소문자 영어가 있음을 의미|`[a-zA-Z] (a, b, A, B)`|
|`[a-z]`|괄호안의 소문자 영어가 있음을 의미|`[a-z] (a, b, c, d...)`|
- 많이 쓸 법한 문법 위주로 정리

### 비고
- 정규식은 예전에 크롤링 프로젝트하면서 몇번 사용해봤는데 contains만 알고 있던 나에겐 신세계였다.
- 문법은 그때 그때 구글링 하는게 편할 듯 싶다. 테스트 해볼수 있는 사이트도 있음.

---
[참고자료(Pupustory)](https://pupustory.tistory.com/132)<br/>
[참고자료(chacha)](https://codechacha.com/ko/java-string-matches/)<br/>
[참고자료(흑곰의 유익한 블로그)](https://m.blog.naver.com/bb_/220863282423)<br/>
[참고자료(RegexPlanet)](https://www.regexplanet.com/advanced/java/index.html)
