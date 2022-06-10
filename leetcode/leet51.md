[문제](https://leetcode.com/problems/n-queens/)
```swift

class Solution {
    // 체스판 크기
    var n = 0
    var arr: [Int] = []
    var answer: [[String]] = []
    
    func solveNQueens(_ n: Int) -> [[String]] {
        self.n = n
        arr = [Int].init(repeating: 0, count: n)
        nQueen(depth: 0)
        
        return answer
    }
    
    func nQueen(depth: Int) {
        // 깊이가 n이면 경우의 수 + 1
        if depth == n {
            answer.append(save(arr: arr))
            return
        }
        // 체스판 크기만큼 반복하며 (depth, i)가 유망한지 검사
        for i in 0..<n {
            // 체스판 depth에 퀸을 놓은 후 유망한지 검사
            arr[depth] = i;
            
            // 유망하다면 다음 depth로 이동
            if possibility(depth: depth) {
                nQueen(depth: depth + 1)
            }
        }
    }
    
    // 해당 depth가 유망한지 검사
    func possibility(depth: Int) -> Bool {
        for i in 0..<depth {
            // 퀸이 같은 세로열에 존재한다면
            if arr[depth] == arr[i] {
                return false
            }
            // 퀸이 대각선에 존재한다면
            // 칸 수 비교로 같으면 대각선에 있다는 뜻
            else if (abs(depth - i) == abs(arr[depth] - arr[i])) {
                return false;
            }
        }
        return true
    }
    
    func save(arr: [Int]) -> [String]{
        let result: [[String]] = [[String]].init(repeating: [String].init(repeating: ".", count: n), count: n)
        var joinedArr: [String] = []
        for i in 0..<arr.count {
            var chars = Array(result)
            chars[i][arr[i]] = "Q"
            let temp = chars[i].joined(separator: "")
            joinedArr.append(temp)
        }
        
        return joinedArr
    }
}

```
