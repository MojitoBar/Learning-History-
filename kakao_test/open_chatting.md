[문제](https://school.programmers.co.kr/learn/courses/30/lessons/42888)

```swift
import Foundation

func solution(_ record:[String]) -> [String] {
     // 유저 id가 key, 닉네임을 value로 갖는 딕셔너리 생성
    var users: [String: String] = [:]
    
    // 결과 배열
    var result: [String] = []
    
    // 들어오는 배열 키 벨류로 먼저 나누기
    
    // 처음 돌면서 닉네임 변경된거 적용
    for i in record {
        let inputs = i.split(separator: " ").map{ $0.description }
        
        // 유저가 들어왔다면
        if inputs[0] == "Enter" {
            users[inputs[1]] = inputs[2]
        }
        if inputs[0] == "Change" {
            users[inputs[1]] = inputs[2]
        }
    }
    
    // 결과 적용
    for i in record {
        let inputs = i.split(separator: " ").map{ $0.description }
        
        if inputs[0] == "Enter" {
            result.append("\(users[inputs[1]]!)님이 들어왔습니다.")
        }
        
        if inputs[0] == "Leave" {
            result.append("\(users[inputs[1]]!)님이 나갔습니다.")
        }
    }
    return result
}
```
