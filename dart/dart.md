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
---
[참고자료(Dart)](https://dart.dev/#try-dart)<br/>
[참고자료(The Coding Papa)](https://www.youtube.com/watch?v=nRsxWt3BWzM&list=PLwUg6hFuXV867frrnqlTeYkuItvgnlilO)
