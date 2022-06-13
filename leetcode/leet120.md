[문제](https://leetcode.com/problems/triangle/submissions/)

### 풀이
2차원 배열로 삼각형 정보를 저장해 DP를 이용해 해결

```swift
class Solution {
    func minimumTotal(_ triangle: [[Int]]) -> Int {
        // 2
        // 3 4
        // 6 5 7
        // 5 1 8 3
        var map: [[Int]] = [[Int]].init(repeating: [Int].init(repeating: 0, count: triangle.last!.count), count: triangle.last!.count)
        
        map[0][0] = triangle[0][0]
        for i in 1..<triangle.count {
            for j in 0..<triangle[i].count {
                if j == 0 {
                    // 맨 왼쪽에 있는놈
                    map[i][0] = map[i - 1][0] + triangle[i][0]
                }
                else if j != 0 && j < triangle[i].count - 1 {
                    // 중간에 있는놈
                    map[i][j] = min((map[i - 1][j] + triangle[i][j]), (map[i - 1][j - 1] + triangle[i][j]))
                }
                else {
                    // 맨 오른쪽에 있는놈
                    map[i][j] = map[i - 1][j - 1] + triangle[i][j]
                }
            }
        }
        return map.last!.min()!
    }
}
```
