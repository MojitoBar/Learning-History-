[문제](https://leetcode.com/problems/binary-tree-cameras/)

### 풀이
dfs를 사용해서 해결

```swift
class Solution {
    var res = 0
    func minCameraCover(_ root: TreeNode?) -> Int {
        return (dfs(root: root) < 1 ? 1 : 0) + res
    }
    func dfs(root: TreeNode?) -> Int {
        if root == nil {
            return 2
        }
        let left = dfs(root: root?.left)
        let right = dfs(root: root?.right)
        
        if left == 0 || right == 0 {
            res += 1
            return 1;
        }
        
        return left == 1 || right == 1 ? 2 : 0
    }
}
```
