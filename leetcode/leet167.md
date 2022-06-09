```swift
class leet167 {
    func twoSum(_ numbers: [Int], _ target: Int) -> [Int] {
        var result: [Int] = []
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
