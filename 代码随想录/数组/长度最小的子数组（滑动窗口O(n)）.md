<https://leetcode.cn/problems/minimum-size-subarray-sum/>

题目描述：

给定一个含有 n 个正整数的数组和一个正整数 s ，找出该数组中满足其和 ≥ s 的长度最小的 连续 子数组，并返回其长度。如果不存在符合条件的子数组，返回 0。

示例：

* 输入：s = 7, nums = [2,3,1,2,4,3]
* 输出：2
* 解释：子数组 [4,3] 是该条件下的长度最小的子数组。

提示：

* 1 <= target <= 10^9
* 1 <= nums.length <= 10^5
* 1 <= nums[i] <= 10^5

解题：

```
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        if sum(nums)<target:
            return 0
        re=len(nums)
        count=0
        left=0
        for right in range(len(nums)):
            count=nums[right]+count
            while count>=target:
                re=min(re,right-left+1)
                count-=nums[left]
                left+=1
        return re
```
根据当前子序列和大小的情况，不断调节子序列的起始位置。

思路：每次找到一个满足条件的组合时，尝试把最左节点删去，希望获得最小满足条件组合

注意：组合长度是right-left+1

