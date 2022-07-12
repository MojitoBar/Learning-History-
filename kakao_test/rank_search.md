[문제](https://school.programmers.co.kr/learn/courses/30/lessons/72412)
```swift
import Foundation

var dic: [String: [Int]] = [:]

func solution(_ info:[String], _ query:[String]) -> [Int] {
    var answer: [Int] = []
    var applicants = [[String]]()
    info.forEach{applicants.append($0.components(separatedBy: " "))}
    applicants.sort{Int($0[4])! < Int($1[4])!}
    
    // 한 지원자에 대해 가능한 모든 경우의 수를 <String: [Int]> 딕셔너리에 저장
    for info in applicants {
        let temp = toString(str: info)
        getCombination(base: temp, arr: ["", "", "", ""], index: 0)
    }
    // 쿼리
    for query in query {
        var temp = toString(str: query.split(separator: " ").map{ $0.description })
        let score = temp.removeLast().description
        if dic[temp.joined()] == nil {
            answer.append(0)
        }else {
            let join = dic[temp.joined()]!
            answer.append(binarySearch(join, Int(score)!))
        }
    }
    return answer
}

func binarySearch(_ scores: [Int],_ queryScore: Int) -> Int {
    if scores.count == 1 {return scores[0] >= queryScore ? 1 : 0}
    if scores.first! >= queryScore {return scores.count }
    if queryScore > scores.last! {return 0 }

    var left = 0
    var right = scores.count

    while left < right {
        let middle = (left + right) / 2
        if scores[middle] >= queryScore {
           right = middle
        }else{
            left =  middle + 1
        }
    }
    return scores.count - left
}

func getCombination(base: [String], arr: [String], index: Int) {
    if index >= 4 {
        let str = arr.joined().description
        var value = dic[str] ?? []
        value.append(Int(base[4])!)
        dic[str] = value
        return
    }
    var arr1 = arr
    var arr2 = arr
    arr1[index] = ("-")
    arr2[index] = (base[index])
    
    getCombination(base: base, arr: arr1, index: index + 1)
    getCombination(base: base, arr: arr2, index: index + 1)
}

func toString(str: [String]) -> [String] {
    let arr = str
    var temp: [String] = []
    for a in 0..<arr.count - 1 {
        if arr[a].description != "and" {
            temp.append(arr[a].first!.description)
        }
    }
    temp.append(arr.last!)
    return temp
}
```
