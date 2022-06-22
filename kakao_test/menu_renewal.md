[문제](https://programmers.co.kr/learn/courses/30/lessons/72411)

### 풀이

조합과 집합을 적절히 사용해야하는 문제.

조합은 생각보다 자주 나오는 기법인 것 같다.

```swift
import Foundation

func solution(_ orders:[String], _ course:[Int]) -> [String] {
    var visited: [Bool]
    
    func combi(n: Int, result: [String], idx: Int, arr: [String]) {
        if result.count < n {
            for i in idx..<arr.count {
                visited[i] = true
                var temp = result
                temp.append(arr[i])
                combi(n: n, result: temp, idx: i + 1, arr: arr)
                visited[i] = false
            }
        }
        // 조합 하나 만들어 졌으면, 집합 연산
        else {
            let tmp = result.sorted(by: <).joined()
            if newDic[tmp] == nil {
                newDic[tmp] = 1
            }
            else {
                newDic[tmp]! += 1
            }
        }
    }
    
    var newDic: [String: Int] = [:]
    
    for i in orders {
        let arr = i.map{ $0.description }
        visited = [Bool].init(repeating: false, count: arr.count)
        for j in course {
            combi(n: j, result: [], idx: 0, arr: arr)
        }
    }
    
    let sortedDic = newDic.sorted { item1, item2 in
        if item1.key.count < item2.key.count {
            return true
        }
        else if item1.key.count == item2.key.count {
            if item1.value > item2.value {
                return true
            }
            return false
        }
        else {
            return false
        }
    }.filter({ item in
        item.value > 1
    })

    var maxValue = 0
    var returnArr: [String] = []
    var answer: [String] = []
    for i in course {
        maxValue = 0
        for j in sortedDic {
            if i == j.key.count {
                if maxValue < j.value {
                    returnArr = []
                    maxValue = j.value
                    returnArr.append(j.key)
                }
                else if maxValue == j.value {
                    returnArr.append(j.key)
                }
            }
        }
        answer += returnArr
    }
    
    // 조합과 집합을 이용해야할듯
    return Set(answer).sorted(by: <)
}
```
