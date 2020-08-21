# Dart 특별편
### 개요
- Flutter개발을 위한 초석 다지기.
- Dart언어를 공부하며 처음 알게된 부분만 작성.
- 계속해서 추가 예정.

## 문자열 출력 중 함수, 변수 사용법
```dart
var dart = 'dart!';

// 기본적인 문자열 출력 방법.
print("Hello dart!");

// 변수를 포함한 문자열 출력 방법.
print("Hello $dart");

String printDart(){
  return "dart!";
}

// 함수를 포함한 문자열 출력 방법.
print("Hello ${printDart()}");
```
- 문자열에 사용하는 큰 따옴표와 작은 따옴표의 차이는 없음.

## 함수 선언 방법
```dart
// 기본적인 함수 선언 법.
int timesTwo(int x){
  return x * 2;
}
// 함수 내용이 한 줄이라면 화살표 함수 선언 가능.
int timesTwo(int x) => x * 2;

// 함수 파라미터로 함수를 받을 수도 있음.
int timesFour(Function f, int x){
 return x = f(x) + f(x);
}

// 마찬가지로 화살표 함수 선언 가능.
int timesFour(Function f, int x) => x = f(x) + f(x);
```

## 클래스
```dart
// 기본적인 클래스 선언.
class Car{
  int seats;
  String color;
  
  Car(int sts, String clr){
    this.seats = sts;
    this.color = clr;
  }
  // 화살표 함수 적용.
  printVars() => print('seat : ${seats}, color : ${color}');
}

main(){
  Car newCar = Car(4, 'red');
  newCar.printVars();
}
```
### 클래스 생성자에 []를 쓴 버전
```dart
class Car{
  int seats;
  String color;
  // 대괄호 안의 파라미터 값은 옵션값이 되어 꼭 넣지 않아도 되는 값이 된다.
  Car(int sts, [String clr]){
    this.seats = sts;
    this.color = clr;
  }
  // 화살표 함수 적용.
  printVars() => print('seat : ${seats}, color : ${color}');
}

main(){
  Car newCar = Car(4);
  // color 부분에서 null을 출력함.
  newCar.printVars();
}
```
### 클래스 생성자에 {}를 쓴 버전
```dart
class Car{
  int seats;
  String color;
  // 중괄호 안의 파라미터 값은 이름에 따라 값을 지정해줄 수 있다. (파라미터 순서에 상관없이 초기화 가능.)
  Car({int sts, String clr}){
    this.seats = sts;
    this.color = clr;
  }
  // 화살표 함수 적용.
  printVars() => print('seat : ${seats}, color : ${color}');
}

main(){
// 파라미터의 이름을 사용해서 값 지정 가능. 순서에 상관없이 파라미터를 쓸 수 있음. 
  Car newCar = Car(sts : 1, clr : 'black');
  newCar.printVars();
}
```
- 클래스 선언시 `new`키워드를 생략할 수 있다. (근데 있는게 보기엔 더 편한듯.)

## Async (비동기) & future
- Dart 코드는 단일 쓰레드에서 실행.
- future는 비동기 작업의 결과를 나타낸다.

### 잘못된 비동기 프로그램
```dart
String createOrderMessage () {
  // getUserOrder() 함수의 작업이 끝나기 전에 order에 값을 넣어버린다.
  var order = getUserOrder();
  return 'Your order is: $order';
}

// 이 함수가 시간이 걸리는 함수라 가정한다.
Future<String> getUserOrder() {
  // Imagine that this function is more complex and slow
  return Future.delayed(Duration(seconds: 4), () => 'Large Latte');
}

main () {
  print(createOrderMessage());
}
```
- `getUserOrder()` 함수가 시간이 걸리게 되면 `order` 변수에 올바른 값을 넘겨줄 수 없다.

### async, await 키워드를 이용한 비동기 프로그램
```dart
// async 키워드를 통해 해당 메소드가 비동기 작업임을 표시.
Future<String> createOrderMessage() async {
  // await 키워들르 통해 `getUserOrder()`가 끝날 때까지 기다림.
  var order = await getUserOrder();
  return 'Your order is: $order';
}

Future<String> getUserOrder() {
  // Imagine that this function is more complex and slow
  return Future.delayed(Duration(seconds: 4), () => 'Large Latte');
}

main() async {
  print("Fetching user order...");
  // return 값이 future이기 때문에 main함수 역시 비동기 작업임을 표시하고 값을 받아 올 때까지 기다림.
  print(await createOrderMessage());
}
```
- 비동기 작업에 대표적인 예로는 네트워크를 통해 데이터를 가져오는경우 (ex 크롤링), 파일 입출력 등이 있다.
- future 키워드는 해당 함수가 비동기 작업이라는 것을 나타낸다고 보면 될것같다.
- 비동기 함수를 사용하는 함수에서는 반드시 async, await 키워드를 사용해야한다.
- 비동기 함수 실행 도중 에러는 `try-catch`문으로 잡으면 된다.
- async, await을 대신해 `future.then`을 사용할 수도 있지만 나는 async, await가 보기 편하다. 나중에 꼭 `future.then`을 사용해야되는 경우가 생기면 그때 다시 보면 될듯.
---
[참고자료(Dart)](https://dart.dev/#try-dart)<br/>
[참고자료(The Coding Papa)](https://www.youtube.com/watch?v=nRsxWt3BWzM&list=PLwUg6hFuXV867frrnqlTeYkuItvgnlilO)<br/>
[참고자료(Beom Dev Log)](https://beomseok95.tistory.com/309#future%EB%9E%80_)
