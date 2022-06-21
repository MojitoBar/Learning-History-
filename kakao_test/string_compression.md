[문제](https://programmers.co.kr/learn/courses/30/lessons/60057)

```swift
func solution(_ s:String) -> Int {
    var result = Int.max
    // 1부터 s/2까지 돌며 그만큼 문자열을 나눈다
    if s.count / 2 < 2 {
        return 1
    }
    for n in 1...s.count / 2 {
        var arr: [String] = []
        for i in stride(from: 0, to: s.count, by: n) {
            var str = ""
            for j in i..<i+n {
                if j < s.count {
                    str += s[s.index(s.startIndex, offsetBy: j)].description
                }
            }
            arr.append(str)
        }
        result = min(check(arr: arr).count, result)
    }
    return result
}

func check(arr: [String]) -> String {
    var start = 0
    var answer = ""
    while start < arr.count {
        var count = 1
        let compare = arr[start]
        for j in stride(from: start + 1, to: arr.count, by: 1) {
            if compare == arr[j] {
                count += 1
            }
            else {
                break
            }
        }
        if count > 1 {
            answer += count.description
            answer += compare
        }
        else {
            answer += compare
        }
        start += count
    }
    return answer
}
```
