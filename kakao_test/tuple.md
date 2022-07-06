[문제](https://school.programmers.co.kr/learn/courses/30/lessons/64065)

```swift
import Foundation

func 튜플(s: String) -> [Int] {
    var inputArr: [[Int]] = []
    var arr = s.components(separatedBy: "},{")
    arr[0].removeFirst()
    arr[0].removeFirst()
    arr[arr.count - 1].removeLast()
    arr[arr.count - 1].removeLast()
    
    for i in arr {
        let temp = i.split(separator: ",").map { Int($0.description)! }
        inputArr.append(temp)
    }
    
    inputArr = inputArr.sorted { i1, i2 in
        return i1.count < i2.count
    }
    
    print(inputArr)
    var answer: [Int] = []
    if inputArr.count == 1 {
        return inputArr[0]
    }
    else {
        answer.append((inputArr.first?.first)!)
        for i in 0..<inputArr.count - 1 {
            let set1: Set<Int> = Set.init(inputArr[i])
            let set2: Set<Int> = Set.init(inputArr[i + 1])
            answer.append(Array(set2.subtracting(set1))[0])
        }
    }
    return answer
}

```
