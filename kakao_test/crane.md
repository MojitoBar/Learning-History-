[문제](https://school.programmers.co.kr/learn/courses/30/lessons/64061)
```swift
import Foundation

var arr: [Int] = []
var answer: Int64 = 0

func solution(_ board:[[Int]], _ moves:[Int]) -> Int64 {
    var board = board
    // moves 반복
    for i in moves{
        for j in 0..<board.count{
            // movies - 1 번째 부터 밑으로 크레인 내리기
            if board[j][i - 1] == 0{
                // 크레인 내리기
                continue
            }
            else{
                // 바구니에 담기
                check(i: board[j][i - 1])
                // 0으로 바꾸기
                board[j][i - 1] = 0
                break
            }
        }
    }
    return answer
}

func check(i: Int){
    // 만약 배열이 비어있지 않다면
    if !arr.isEmpty{
        // 만약 마지막 인형과 넣을 인형이 같다면
        if arr.last == i{
            arr.removeLast()
            answer += 2
        }
    (    else{
            arr.append(i)
        }
    }
    // 만약 배열이 비어있다면
    else{
        arr.append(i)
    }
}
```
