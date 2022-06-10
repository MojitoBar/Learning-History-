[문제](Merge Sorted Array)
```swift
class Solution {
    func merge(_ nums1: inout [Int], _ m: Int, _ nums2: [Int], _ n: Int) {
        for i in 0..<nums2.count {
            nums1[m + i] = nums2[i]
        }
        nums1 = nums1.sorted(by: <)
    }
}
```
