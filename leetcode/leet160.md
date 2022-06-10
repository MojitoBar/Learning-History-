[문제](https://leetcode.com/problems/intersection-of-two-linked-lists/)
```swift
class Solution {
    func getIntersectionNode(_ headA: ListNode?, _ headB: ListNode?) -> ListNode? {
        guard headA != nil, headB != nil else { return nil }

        var a: ListNode? = headA
        var b: ListNode? = headB

        while a !== b {
            a = a == nil ? headB : a?.next
            b = b == nil ? headA : b?.next
        }

        return a
    }
}
```
