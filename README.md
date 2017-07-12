# leetcode_day_by_day (C language)
## Day 01 Remove Duplicates from Sorted Array
Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.
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
