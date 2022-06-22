[문제](https://programmers.co.kr/learn/courses/30/lessons/81301)

```swift
import Foundation

func solution(_ s:String) -> Int {
    // 아이디어
    // 1. 반복문을 돌며 검사할 문자를 만든다
    // 2. contains를 이용해 숫자로 변경한다.
    // 3. result를 만든다
    
    let dic: [String: String] = ["zero": "0",
                                 "one": "1",
                                 "two": "2",
                                 "three": "3",
                                 "four": "4",
                                 "five": "5",
                                 "six": "6",
                                 "seven": "7",
                                 "eight": "8",
                                 "nine": "9"]
    var search = ""
    var answer = ""
    for i in s {
        if let number = Int(i.description) {
            answer += number.description
        }
        else {
            search += i.description
            if dic[search] != nil {
                answer += dic[search]!
                search = ""
            }
        }
    }
    return Int(answer)!
}
```
