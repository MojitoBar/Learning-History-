[문제](https://leetcode.com/problems/range-sum-query-2d-immutable/)

```swift
class NumMatrix {
    let preSum: [[Int]]
    
    init(_ matrix: [[Int]]) {
        let m = matrix.count
        let n = matrix[0].count
        var result = Array(repeating: Array(repeating: 0, count: n+1), count: m+1)
        
        for i in 1...m {
            for j in 1...n {
                result[i][j] = result[i-1][j] + result[i][j-1] - result[i-1][j-1] + matrix[i-1][j-1]
            }
        }
        self.preSum = result
    }
    
    func sumRegion(_ row1: Int, _ col1: Int, _ row2: Int, _ col2: Int) -> Int {
        return preSum[row2+1][col2+1] - preSum[row1][col2+1] - preSum[row2+1][col1] + preSum[row1][col1]
    }
}

```
