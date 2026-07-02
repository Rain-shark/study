<https://leetcode.cn/problems/squares-of-a-sorted-array/>

题目描述：

给你一个按 非递减顺序 排序的整数数组 nums，返回 每个数字的平方 组成的新数组，要求也按 非递减顺序 排序。

示例 1：

* 输入：nums = [-4,-1,0,3,10]
* 输出：[0,1,9,16,100]
* 解释：平方后，数组变为 [16,1,0,9,100]，排序后，数组变为 [0,1,9,16,100]

示例 2：

* 输入：nums = [-7,-3,2,3,11]
* 输出：[4,9,9,49,121]

暴力求解：

```
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        i=0
        while i<len(nums):
            nums[i]=nums[i]*nums[i]
            i+=1
        nums.sort()
        return nums
```
双指针法：

```
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        a=0
        b=len(nums)-1
        k=len(nums)-1
        result=[0]*(len(nums))
        while k>=0:
            if nums[a]*nums[a]>= nums[b]*nums[b]:
                result[k]=nums[a]*nums[a]
                a+=1
            elif nums[a]*nums[a]<nums[b]*nums[b]:
                result[k]=nums[b]*nums[b]
                b-=1
            k-=1
        return result
```
注意：

1. 双指针重新构建一个数组，不能result=[]，这样不能按索引赋值，应result=[0]\*l
2. 双指针思想是左右两边平方值一定是最大的，所以k=l-1，从数组最右开始构建
3. if-if 中如果判断条件有更改可能导致两重判断，这类最好用 if-elif
