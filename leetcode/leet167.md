[문제](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
```swift
// 주어진 배열에서 2개를 더해 target을 만들기
class leet167 {
    func twoSum(_ numbers: [Int], _ target: Int) -> [Int] {
        var result: [Int] = []
        // 반복문 두번 돌면서 브루트포스
        for i in 0..<numbers.count {
            for j in i + 1..<numbers.count {
                if target == numbers[i] + numbers[j] {
                    result.append(i + 1)
                    result.append(j + 1)
                    return result
                }
            }
        }
        return []
    }
}

```
