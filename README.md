# leetcode_day_by_day (Swift)
## Day-01 : Remove Duplicates from Sorted Array
Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.
C:
```
int removeDuplicates(int* nums, int numsSize) {
        if (numsSize == 0) return 0;
        int index = 1;
        for (int i = 1; i < numsSize; i++) {
            if (nums[i] != nums[index-1])
                nums[index++] = nums[i];
        }
        return index;
}
```
Swift:
```
func removeDuplicates(_ nums:[Int], _ numsSize: Int) -> Int {
    var nums = nums
    if numsSize == 0 {
        return 0
    }
    var index = 1
    for i in 1..<numsSize {
        if nums[i] != nums[index - 1] {
            nums[index] = nums[i]
            index = index + 1
        }
    }
    return index
}
```
## Day-02 : Two Sum
Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
Solution:
创建一个字典，以便于快速查询
```
func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
    var dict = [Int: Int]()
    var array: [Int] = [0, 0]
    for i in 0..<nums.count {
        let look = target - nums[i]
        if let index = dict[look] {
            array = [i,index]
        } else {
            dict.updateValue(i, forKey: nums[i])
        }
    }
    return array
}

```

## Day-03 : Add Two Numbers
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
> 关键点分析：head初始化及移动，进位处理，next结束处理。

代码：
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public var val: Int
 *     public var next: ListNode?
 *     public init(_ val: Int) {
 *         self.val = val
 *         self.next = nil
 *     }
 * }
 */
class Solution {
    func addTwoNumbers(_ l1: ListNode?, _ l2: ListNode?) -> ListNode? {
         var l2 = l2
    var l1 = l1
    var head = ListNode(0)
    var node = head
    var number = 0

    while l1 != nil || l2 != nil {
        let sum = (l1?.val)! + (l2?.val)! + number
        number = sum / 10
        node.next = ListNode(sum % 10)
        node = node.next!
        l1 = l1?.next
        l2 = l2?.next
    }
    if number > 0 {
        node.next = ListNode(number)
    }
    return head.next
    }
}
```
## Day-04 : Longest Substring Without Repeating Characters
Given a string, find the length of the longest substring without repeating characters.

Examples:

Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
> 分析：找到当前的index，和前一个记住的preIndex，相减，以下swift代码超时了，通不过leetcode提交。
```
func lengthOfLongestSubstring(_ s: String) -> Int {
    var distance = 0
    let len = s.characters.count
    if len == 1 {
        return 1
    }
    var dict = [Character: Int]()
    var preIndex = 0
    for j in 0 ..< len {
        let str = s[s.index(s.startIndex, offsetBy: j)]
        if let d = dict[str] {
            preIndex = max(preIndex, d)
        }
        distance = max(j - preIndex + 1, distance)
        dict.updateValue(j + 1, forKey: str)
    }
    return distance
}
```


