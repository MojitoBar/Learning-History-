# Dart 특별편
### 개요
- Flutter개발을 위한 초석 다지기.
- Dart언어를 공부하며 처음 알게된 부분만 작성.
- 계속해서 추가 예정.

### 문자열 출력 중 함수, 변수 사용법
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

### 함수 선언 방법
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

### 클래스
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
#### 클래스 생성자에 []를 쓴 버전
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
#### 클래스 생성자에 {}를 쓴 버전
```dart
class Car{
  int seats;
  String color;
  // 대괄호 안의 파라미터 값은 옵션값이 되어 꼭 넣지 않아도 되는 값이 된다.
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
---
[참고자료(Dart)](https://dart.dev/#try-dart)<br/>
[참고자료(The Coding Papa)](https://www.youtube.com/watch?v=nRsxWt3BWzM&list=PLwUg6hFuXV867frrnqlTeYkuItvgnlilO)
