
<https://leetcode.cn/problems/binary-search/>

题目描述：

给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

示例 1:

```
输入: nums = [-1,0,3,5,9,12], target = 9
输出: 4
解释: 9 出现在 nums 中并且下标为 4
```
示例 2:

```
输入: nums = [-1,0,3,5,9,12], target = 2
输出: -1
解释: 2 不存在 nums 中因此返回 -1
```
提示：

你可以假设 nums 中的所有元素是不重复的。

n 将在 [1, 10000]之间。

nums 的每个元素都将在 [-9999, 9999]之间。

![](二分查找(O(log_n))_001.jpg)

首先是有序数组，然后主要确定循环边界问题

我设置定义 target 是在一个在左闭右开的区间里，也就是[left, right)

left=0, right=len(nums)

while语句中left<right；因为left=right不满足[left, right) 区间定义

当 target<nums[middle]时，设置right=middle, 因为right需要取不到

当 target>nums[middle]时，设置left=middle+1，

注意：python3中‘/’会除出浮点数，‘//’才是整除

```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums)
        while left<right:
            middle = (left+right)//2
            if target<nums[middle]:
                right=middle
            if target>nums[middle]:
                left =middle+1
            if target==nums[middle]:
                return middle
        return -1
```
