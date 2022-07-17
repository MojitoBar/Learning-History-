[문제](https://school.programmers.co.kr/learn/courses/30/lessons/92335)
```swift
import Foundation

func solution(_ n:Int, _ k:Int) -> Int {
    let str = change(N: n, K: k)
    let arr = str.getArrayAfterRegex(regex: "[1-9]+")
    var result = 0
    
    for i in arr {
        if checkPrime(N: UInt64(i)!) {
            result += 1
        }
    }
    
    return result
}

// K진수로 변환 함수
func change(N: Int, K: Int) -> String {
    var arr: [String] = []
    var n = N
    while true {
        if n / K < K {
            arr.insert((String(n % K)), at: 0)
            arr.insert((String(n / K)), at: 0)
            break
        }
        arr.insert((String(n % K)), at: 0)
        n /= K
    }
    return arr.joined()
}

// N이 소수인지 판별하는 함수
func checkPrime(N: UInt64) -> Bool {
    if N == 2 || N == 3{
        return true
    }
    else if N == 0 || N == 1 {
        return false
    }
    let n = UInt64(sqrt(Double(N)))
    for i in 2...n {
        if N % UInt64(i) == 0 {
            return false
        }
    }
    return true
}

extension String {
    func getArrayAfterRegex(regex: String) -> [String] {
        do {
            let regex = try NSRegularExpression(pattern: regex)
            let results = regex.matches(in: self, range: NSRange(self.startIndex..., in: self))
            return results.map {
                String(self[Range($0.range, in: self)!])
            }
        } catch let error {
            print(error)
            return []
        }
    }
}
```
