[문제](https://programmers.co.kr/learn/courses/30/lessons/72410)

```swift
import Foundation

func solution(_ new_id:String) -> String {
    
//    아이디의 길이는 3자 이상 15자 이하여야 합니다.
//    아이디는 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.) 문자만 사용할 수 있습니다.
//    단, 마침표(.)는 처음과 끝에 사용할 수 없으며 또한 연속으로 사용할 수 없습니다.

//    1단계 new_id의 모든 대문자를 대응되는 소문자로 치환합니다.
    let lower = new_id.lowercased()
//    2단계 new_id에서 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.)를 제외한 모든 문자를 제거합니다.
    let filter = lower.filter { "abcdefghijklmnopqrstuvwxyz0123456789-_.".contains($0) }
//    3단계 new_id에서 마침표(.)가 2번 이상 연속된 부분을 하나의 마침표(.)로 치환합니다.
    var removeDot = filter
    while true {
        if removeDot.range(of: "[.]{2,}", options: .regularExpression) != nil {
            removeDot = removeDot.replacingOccurrences(of: "..", with: ".")
        }
        else {
            break
        }
    }
//    4단계 new_id에서 마침표(.)가 처음이나 끝에 위치한다면 제거합니다.
    if removeDot.first == "." {
        removeDot.removeFirst()
    }
    if removeDot.last == "." {
        removeDot.removeLast()
    }
//    5단계 new_id가 빈 문자열이라면, new_id에 "a"를 대입합니다.
    if removeDot == "" {
        removeDot += "a"
    }
//    6단계 new_id의 길이가 16자 이상이면, new_id의 첫 15개의 문자를 제외한 나머지 문자들을 모두 제거합니다.
    var lengthCheck = removeDot
    if lengthCheck.count > 15 {
        var end = lengthCheck.index(removeDot.startIndex, offsetBy: 15)
        lengthCheck = String(lengthCheck[lengthCheck.startIndex..<end])
        // 만약 제거 후 마침표(.)가 new_id의 끝에 위치한다면 끝에 위치한 마침표(.) 문자를 제거합니다.
        if lengthCheck.last == "." {
            lengthCheck.removeLast()
        }
    }
//    7단계 new_id의 길이가 2자 이하라면, new_id의 마지막 문자를 new_id의 길이가 3이 될 때까지 반복해서 끝에 붙입니다.
    while true {
        if lengthCheck.count < 3 {
            lengthCheck += lengthCheck.last!.description
        }
        else {
            break
        }
    }
    return lengthCheck
}
```
