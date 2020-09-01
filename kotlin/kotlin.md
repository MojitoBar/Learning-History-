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

### 조건문 if-else, when
```kotlin
fun maxBy(a:Int, b:Int):Int{
    if(a > b){
        return a
    }else{
        return b
    }
}

fun maxBy2(a:Int, b:Int) = if(a>b) a else b

fun checkNum(score:Int){
    when(score){
        0 -> println("this is 0")
        1 -> println("this is 1")
        2, 3 -> println("this is 2 or 3")
        in 10..80 -> println("not bad")
        in 90..100 -> println("you are genius")
        else -> println("I don't know")
    }
    
    var b = when(score){
        1 -> 1
        2 -> 2
        else -> 3
    }
}
```
- if문의 사용은 다른 언어와 크게 다르지 않다.
- 간략하게 줄이는 방법이 조금 다른데, `maxBy2()`함수를 보면 함수의 리턴값을 자동으로 추론하기 때문에 따로 선언해주지 않아도 된다.
- when문은 다른 언어의 switch문과 비슷하다.
- `when(변수){}`형태로 사용하며, 중괄호 안에서는 화살표를 통해 특정 값일 때 행동을 선언해줄 수 있다.
- when문을 사용할때 무조건 else를 써줘야 한다.
- `in` 키워드를 통해 범위를 지정할 수도 있다.
- 화살표로 행동을 지정해주는 것을 return값으로 사용해줄수도 있다.

### Array, List
```kotlin
fun array(){
    val array = arrayOf(1,2,3)
    val list = listOf(1,2,3)
    
    val array2 = arrayOf(1,"d",2.3f)
    val list2 = listOf(1,"d",11L)
    
    array[0] = 3
    var result = list.get(0)
    
    val arrayList = arrayListOf<Int>()
    arrayList.add(10)
    arrayList.add(20)
}
```
- array는 기본적으로 mutable이고 list는 기본적으로 immutable이다.
- array는 arrayOf로, list는 listOf로 초기화 한다.
- array는 읽기, 쓰기 둘다 가능하지만 list는 읽기 전용이기 때문에 `list.get()`으로 통해 값을 가져올 수만 있다.
- list의 원소는 주소값을 참조하는 것이기 때문에 `val`로 선언해도 된다.
- 하지만 list를 새로 초기화하거나 list 자체를 덮어 씌울 경우 `var`로 선언해야 한다.
- mutable list도 있다고 한다.

### For, While 반복문
```kotlin
fun forAndWhile(){
    val students = arrayListOf("mojito", "watermelon", "strawberry", "peach")
    for(name in students){
        println(name)
    }
    
    var sum : Int = 0
    for(i in 1..100){
        sum += i
    }
    println(sum)
    
    for((index, name) in students.withIndex()){
        println("${index+1}번째 학생 : ${name}")
    }
    
    var index = 0
    while(index < 10){
        println("current index : ${index}")
        index++
    }
}
```
- for문과 while문의 작동 방식은 다른 언어와 비슷하다.
- for문에서는 `in`키워드로 범위를 지정해준다.
- for문에서 index를 함께 지정해줄 수 있는데 `in`뒤에 `withIndex()`를 추가해줘야한다.
- `1..100`같은 방식 외에도 `downTo`, `step`, `until`같은 키워드도 있다.

### Nullable, NonNull
```kotlin
fun nullcheck(){
    //NPE :NULL pointer Exception
    var name : String = "mojito"
    var nullName : String? = null
    var nameInUpperCase = name.toUpperCase()
    var nullNameInUpperCase = nullName?.toUpperCase()
    
    //?:
    val lastName : String? = "Ju"
    val fullName = name + " " + (lastName?: "NO lastName")
    
    println(fullName)
}

fun ignoreNulls(str : String?){
    //!!
    val mNotNull : String = str!!
    val upper = mNotNull.toUpperCase()
    
    val email : String? = "mojito@naver.com"
    email?.let{
    	println("my email is ${email}")   
    }
}
```
- 코틀린에는 변수가 null이 될 수 있는지, null이 될 수 없는지 지정해줄 수 있다.
- `var variable : String?` 자료형 뒤에 ?를 붙히는 것으로 해당 변수가 null일수도 있다는 것을 암시한다.
- 해당 변수가 nullable이면 `toUpperCase()`와 같은 함수를 사용하기 위해 `nullName?.toUpperCase()`처럼 변수뒤에 ?를 붙혀줘야한다.
- `?:`키워드는 엘비스 연산자라 불린다. 90도로 돌리면 ?가 엘비스 머리 같단다..
- `?:`키워드는 해당 변수가 nullable일때 기본값을 지정해 줄 수 있다.
- `!!`키워드는 해당 변수가 nullable이지만 null이 아니라고 보장해주는 키워드이다.
- null이 아니라고 보장되면 `toUpperCase()`와 같은 함수를 사용하기위해 변수뒤에 ?를 붙혀주지 않아도 된다.
---
[참고자료(Code with Joyce)](https://www.youtube.com/watch?v=IDVnZPjRCYg)<br/>
[참고자료(Kotlin)](https://play.kotlinlang.org/)
