[문제](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
### 해설
스트링을 이중 반복문으로 돌며 브루트포스로 해결

```swift
import Foundation
class leet3 {
    func lengthOfLongestSubstring(_ s: String) -> Int {
        let stringArr = s.map{ $0.description }
        var set: Set<String> = []
        var long = 0
        
        for i in 0..<stringArr.count {
            for j in i..<stringArr.count {
                // 중복된다면
                if set.contains(stringArr[j]) {
                    break
                }
                // 중복 안되면
                else {
                    set.insert(stringArr[j])
                }
            }
            long = max(long, set.count)
            set = []
        }
        
        return long
    }
}
```
