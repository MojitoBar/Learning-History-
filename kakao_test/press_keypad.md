[문제](https://programmers.co.kr/learn/courses/30/lessons/67256)

```swift
import Foundation

func getDistance(left: (Int, Int), right: (Int, Int), go: (Int, Int)) -> String {
    if abs(left.0 - go.0) + abs(left.1 - go.1) < abs(right.0 - go.0) + abs(right.1 - go.1) {
        return "L"
    }
    else if abs(left.0 - go.0) + abs(left.1 - go.1) > abs(right.0 - go.0) + abs(right.1 - go.1) {
        return "R"
    }
    else {
        return "S"
    }
}

func solution(_ numbers:[Int], _ hand:String) -> String {
    // 1 4 7 은 무조건 왼손
    // 3 6 9 는 무조건 오른손
    
    var result = ""
    var preNum = -1
    var leftIdx = 10
    var rightIdx = 11
    let numIdx: [(Int, Int)] = [(3, 1), (0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2), (2, 0), (2, 1), (2, 2), (3, 0), (3, 2)]
    
    for n in numbers {
        if n == 1 || n == 4 || n == 7 {
            result += "L"
            leftIdx = n
        }
        else if n == 3 || n == 6 || n == 9 {
            result += "R"
            rightIdx = n
        }
        else {
            // 내가 왼손잡이이면
            if hand == "left" {
                // 만약 이전 숫자가 없다면
                if preNum == -1 {
                    result += "L"
                    leftIdx = n
                }
                else {
                    let tmp = getDistance(left: numIdx[leftIdx], right: numIdx[rightIdx], go: numIdx[n])
                    if tmp == "S" {
                        result += "L"
                        leftIdx = n
                    }
                    else {
                        result += tmp
                        if tmp == "L" {
                            leftIdx = n
                        }
                        else {
                            rightIdx = n
                        }
                    }
                }
            }
            // 내가 오른손 잡이이면
            else {
                // 만약 이전 숫자가 없다면
                if preNum == -1 {
                    result += "R"
                    rightIdx = n
                }
                else {
                    let tmp = getDistance(left: numIdx[leftIdx], right: numIdx[rightIdx], go: numIdx[n])
                    if tmp == "S" {
                        result += "R"
                        rightIdx = n
                    }
                    else {
                        result += tmp
                        if tmp == "L" {
                            leftIdx = n
                        }
                        else {
                            rightIdx = n
                        }
                    }
                }
            }
        }
        preNum = n
    }
    
    return result
}
```
