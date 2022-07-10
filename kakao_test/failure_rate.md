[문제](https://school.programmers.co.kr/learn/courses/30/lessons/42889)
```swift
import Foundation

func solution(_ N:Int, _ stages:[Int]) -> [Int] {
    
    // stage는 플레이어가 머무르고 있는 상태 배열
    
    // N은 총 스테이지 개수
    
    // 각 스테이지 별 통과한 사람 메모 배열
    var passArr: [Int] = [Int].init(repeating: 0, count: N + 1)
    var arriveArr: [Int] = [Int].init(repeating: 0, count: N + 1)
    var failArr: [Int:Double] = [:]
    // 각 스테이지를 통과한 숫자
    for stage in stages {
        for j in 1...N {
            if j < stage {
                passArr[j] += 1
            }
        }
    }
    
    // 각 스테이지를 통과한 숫자
    for stage in stages {
        for j in 0...N {
            if j <= stage {
                arriveArr[j] += 1
            }
        }
    }
    
    // 실패율 계산
    for i in 1...N {
        failArr[i] = Double(arriveArr[i] - passArr[i]) / Double(arriveArr[i])
    }
    
    var resultDic = failArr.sorted { item1, item2 in
        if item1.value < item2.value {
            return false
        }
        else if item1.value > item2.value {
            return true
        }
        else {
            if item1.key < item2.key {
                return true
            }
            else {
                return false
            }
        }
    }
    var resultArr: [Int] = []
    for element in resultDic {
        resultArr.append(element.key)
    }
    return resultArr
}
```
