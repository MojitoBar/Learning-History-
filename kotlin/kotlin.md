# Kotlin 기본편
### 개요
- Android 개발을 위한 Kotlin 공부.
- Flutter는 서브, Kotlin을 주력으로 가져갈 예정.
- 계속해서 추가 예정.

### 함수
```kotlin
fun main() {
    helloWorld()
    println(add(4, 5))
}

fun helloWorld(){
    println("Hello World!")
}

fun add(a : Int, b : Int) : Int{
    return a+b
}
```
- 함수 기본 선언은 `fun FunctionName(){}`으로 한다.
- 함수에 매개변수를 쓸땐, `a : Int`형식으로 변수명 뒤에 자료형으로 선언한다.
- 마찬가지로 함수 리턴값 역시 `fun FunctionName() : Int{}`형식으로 함수 뒤에 리턴값 자료형이 온다.

### val vs var
```kotlin
fun hi(){
	  val a : Int = 10
    var b : Int = 9
    
    val c = 100
    var d = 100
    
    var e : Int
    
    b = 100
    
    var name = "mojito"
}
```
- 매개변수를 선언한것처럼 일반 변수역시 똑같은 포멧으로 선언한다.
- 변수에 바로 값을 지정해주는 경유 `: Int`를 생략해줄 수 있다.
- val은 value의 약자로 값을 한번 지정해주면 바꿀 수 없다.
- var은 variable의 약자로 값이 언제든지 변할 수 있다.
- 만약 변수를 선언하고 바로 값을 지정해주지 않는다면 뒤에 `: Int`등 자료형을 꼭 써줘야한다.

### String Template
```kotlin
fun main() {
    val name = "Mojito"
    val lastName = "bar"
    
    println("my name is ${name + lastName} I'm 23")
    println("this is 2\$a")
}
```
- 변수를 문자열과 같이 출력하려면 `$`뒤에 변수 명을 사용한다.
- `${}`중괄호 안에 있는 것을 변수로 취급한다.
- `$`를 문자 그대로 사용하고 싶으면 역슬래쉬와 함께쓰면 된다.


---
[참고자료(Code with Joyce)](https://www.youtube.com/watch?v=IDVnZPjRCYg)<br/>
[참고자료(Kotlin)](https://play.kotlinlang.org/)
