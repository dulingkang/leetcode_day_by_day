# leetcode_day_by_day (Swift)
## Day 01 Remove Duplicates from Sorted Array
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
## Day 02 Two Sum
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
