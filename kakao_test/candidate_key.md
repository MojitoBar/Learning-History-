[문제](https://programmers.co.kr/learn/courses/30/lessons/42890)

### 풀이
조합과 집합연산을 잘 활용할 것.

```swift
import Foundation

func solution(_ relation:[[String]]) -> Int {
    // 컬럼 갯수
    var columnCount = relation[0].count
    // 로우 갯수
    let rowCount = relation.count
    // 순열을 위한 컬럼 배열
    var columnArr: [Int] = []
    // 새로 정의할 컬럼 배열
    var columns: [[String]] = [[String]].init(repeating: [], count: columnCount)
    
    var answer = 0
    
    var answerArr: [[Int]] = []
    // 릴레이션을 반복하면서 컬럼별로 나누기
    
    for i in 0..<columnCount {
        columnArr.append(i)
    }
    
    for i in 0..<columnCount {
        for j in 0..<relation.count {
            columns[i].append(relation[j][i])
        }
    }
    
    func isKey(arr: [String]) -> Bool {
        // 후보키 찾기
        // 중복제거
        let removeDuplicate: Set<String> = Set(arr)
        if removeDuplicate.count == rowCount {
            return true
        }
        return false
    }
    
    
    // 조합
    
//    print(columnArr)
//    print(columns)
    
    var visited: [Bool] = [Bool].init(repeating: false, count: columnCount)
    func combination(pick: Int, result: [Int], curIdx: Int) {
        // ex) 2개를 뽑는다면
        if pick > result.count {
            for i in curIdx..<columnCount {
                if !visited[i] {
                    var temp = result
                    temp.append(columnArr[i])
                    visited[i] = true
                    combination(pick: pick, result: temp, curIdx: i)
                    visited[i] = false
                }
            }
        }
        else {
//            print(result)
            // 해당 조합이 후보키인지.
            var tempString: [String] = []
            for i in 0..<rowCount {
                var str = ""
                for j in result {
                    str += columns[j][i]
                }
                tempString.append(str)
            }
            
//            print(tempString)
            if isKey(arr: tempString) {
                answer += 1
                answerArr.append(result)
            }
        }
    }
    
    
    for i in 1...columnCount {
        combination(pick: i, result: [], curIdx: 0)
        visited = [Bool].init(repeating: false, count: columnCount)
    }
    
    var tempArr = answerArr
    var temp2Arr: [[Int]] = []
    for i in 0..<answerArr.count {
        for j in i + 1..<tempArr.count {
            let set1 = Set(answerArr[i])
            let set2 = Set(tempArr[j])
            let set3 = set1.subtracting(set2)
            
            if set3.count == 0 {
                tempArr[j] = []
            }
        }
    }
    var answerCount = 0
    for i in tempArr {
        if i != [] {
            answerCount += 1
        }
    }
    
    return answerCount
}
```
