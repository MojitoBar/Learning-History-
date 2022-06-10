[문제](https://leetcode.com/problems/roman-to-integer/)
```swift
class Solution {
    func romanToInt(_ s: String) -> Int {
        let dic: [String: Int] = ["I": 1, "V": 5, "X": 10, "L": 50,
                              "C": 100, "D": 500, "M": 1000]
    
        var result = 0
        let array: [String] = s.map{ $0.description }

        var i = 0
        // 스트링을 반복문 돌면서
        while i < array.count {
            // 특이 케이스 판별
            if i < array.count - 1 {
                if array[i] == "I" {
                    if array[i + 1] == "V" || array[i + 1] == "X" {
                        result += (dic[array[i + 1]]! - 1)
                        i += 2
                        continue
                    }
                }
                if array[i] == "X" {
                    if array[i + 1] == "L" || array[i + 1] == "C" {
                        result += (dic[array[i + 1]]! - 10)
                        i += 2
                        continue
                    }
                }
                if array[i] == "C" {
                    if array[i + 1] == "D" || array[i + 1] == "M" {
                        result += (dic[array[i + 1]]! - 100)
                        i += 2
                        continue
                    }
                }
                result += dic[array[i]]!
            }
            else {
                result += dic[array[i]]!
            }
            i += 1
        }

        return result
    }
}
```
