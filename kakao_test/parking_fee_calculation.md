### [문제](https://programmers.co.kr/learn/courses/30/lessons/92341)

##### 문제 해결 순서
1. 먼저 들어온 입/출차 기록을 입차, 출차 기록으로 나눈다.
2. 이중 반복문을 돌며 입차한 차량 번호가 출차 기록에 있는지 확인한다.
3. 있다면 그 시간 차이를 차량번호를 키로하는 딕셔너리에 저장한다. 이때 확인된 출차 기록은 출차 기록 배열에서 삭제한다.
4. 없다면 23:59를 출차 시간으로 보고 그 시간 차이를 같은 딕셔너리에 저장한다.
5. 딕셔너리를 돌며 주차요금을 계산한다.

```swift
import Foundation

func solution(_ fees:[Int], _ records:[String]) -> [Int] {
    var inArr: [(String, String)] = []
    var outArr: [(String, String)] = []
    var sumPrice: [String: Int] = [:]

    for i in 0..<records.count {
        let info = records[i].split(separator: " ").map{ $0.description }
        // 들어온 차량 정보 저장
        if info[2] == "IN" {
            inArr.append((info[1], info[0]))
        }
        // 나간 차량 정보 저장
        else {
            outArr.append((info[1], info[0]))
        }
    }

    // 들어온 차량 배열을 돌며 언제 나갔는지 체크
    for i in 0..<inArr.count {
        // 차량 번호로 찾기
        // 찾았냐?
        var isFind = false
        for j in 0..<outArr.count {
            // 차량 번호가 같다면
            if inArr[i].0 == outArr[j].0 {
                if sumPrice[inArr[i].0] != nil {
                    sumPrice[inArr[i].0]! += getTime(t1: inArr[i].1, t2: outArr[j].1)
                }
                else {
                    sumPrice[inArr[i].0] = getTime(t1: inArr[i].1, t2: outArr[j].1)
                }
                outArr.remove(at: j)
                isFind = true
                break
            }
        }
        // 입차는 있는데 출차가 없다면
        if !isFind {
            if sumPrice[inArr[i].0] != nil {
                sumPrice[inArr[i].0]! += getTime(t1: inArr[i].1, t2: "23:59")
            }
            else {
                sumPrice[inArr[i].0] = getTime(t1: inArr[i].1, t2: "23:59")
            }
        }
    }


    var result:[Int] = []

    let sortedPrice = sumPrice.sorted { e1, e2 in
        e1.key < e2.key
    }
    // 주차요금 계산
    for i in sortedPrice {
        // 만약 기본 시간을 넘었다면
        if i.value > fees[0] {
            let 몫 = (i.value - fees[0]) / fees[2]
            let 나머지 = (i.value - fees[0]) % fees[2]
            var price = 몫 * fees[3] + fees[1]
            if 나머지 > 0 {
                price += fees[3]
            }
            result.append(price)
        }
        else {
            result.append(fees[1])
        }
    }
    return result
}

func getTime(t1: String, t2: String) -> Int {
    let info1 = t1.split(separator: ":").map{ Int($0)! }
    let info2 = t2.split(separator: ":").map{ Int($0)! }

    let time1 = info1[0] * 60 + info1[1]
    let time2 = info2[0] * 60 + info2[1]

    return time2 - time1
}```
