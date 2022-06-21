[문제](https://programmers.co.kr/learn/courses/30/lessons/92334)
```swift
import Foundation

func solution(_ id_list:[String], _ report:[String], _ k:Int) -> [Int] {
    // 유저 리스트, 신고 내역 리스트, 기준이 되는 신고 횟수
    
    // 정답 배열
    var answer: [Int] = []
    
    // 중복 신고 필터 set
    let noDuplicateReport: Set<String> = Set(report)
    
    // 신고를 받은 횟수를 체크할 딕셔너리
    var reportDic: [String: Int] = [:]
    for i in id_list {
        reportDic[i] = 0
    }
    
    // 유저별 신고한 아이디를 저장할 딕셔너리
    var userReportDic: [String: [String]] = [:]
    for i in id_list {
        userReportDic[i] = []
    }
    
    
    // 신고 횟수 카운트
    for i in noDuplicateReport {
        // info[0] = 신고한 유저, info[1] = 신고당한 유저
        let info = i.split(separator: " ").map{ $0.description }
        
        // 유저가 신고한 아이디 추가
        userReportDic[info[0]]!.append(info[1])
        
        // 신고 당한 유저 카운트 증가
        reportDic[info[1]]! += 1
    }
    
    // 정지할 유저 배열
    var exitUser: [String] = []
    
    // 정지된 유저 찾기
    for i in reportDic {
        // 기준 이상으로 신고 당했다면
        if i.value >= k {
            exitUser.append(i.key)
        }
    }
    
    for i in id_list {
        let a = Set(userReportDic[i]!)
        let b = Set(exitUser)
        
        answer.append(a.intersection(b).count)
    }
    return answer
}
```
