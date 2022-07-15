[문제](https://school.programmers.co.kr/learn/courses/30/lessons/17684)

```swift
import Foundation

func solution(_ msg:String) -> [Int] {
    // 색인 번호 배열
    var indexArr: [String: Int] = ["A": 1, "B": 2, "C": 3, "D": 4, "E": 5, "F": 6,
                                   "G": 7, "H": 8, "I": 9, "J": 10, "K": 11, "L": 12,
                                   "M": 13, "N": 14, "O": 15, "P": 16, "Q": 17, "R": 18,
                                   "S": 19, "T": 20, "U": 21, "V": 22, "W": 23, "X": 24, "Y": 25, "Z": 26]
    
    let msgArr = msg.map { $0.description }
    var indexCount = 26
    var answer: [Int] = []
    
    func printIndex(msgArr: [String], msg: String, index: Int) {
        if index < msgArr.count - 1 {
            if indexArr[msg + msgArr[index + 1]] != nil {
                printIndex(msgArr: msgArr, msg: msg + msgArr[index + 1], index: index + 1)
            }
            // 딕셔너리에 없으면 이전에 있던 글자 색인 출력 후 뒤에 없는 글자 색인 추가
            else {
                answer.append(indexArr[msg]!)
                indexCount += 1
                indexArr[msg + msgArr[index + 1]] = indexCount
                printIndex(msgArr: msgArr, msg: msgArr[index + 1], index: index + 1)
            }
        }
        else {
            answer.append(indexArr[msg]!)
            return
        }
    }
    
    printIndex(msgArr: msgArr, msg: msgArr[0], index: 0)
    
    return answer
}

```
