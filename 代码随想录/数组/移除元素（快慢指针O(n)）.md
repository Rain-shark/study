<https://leetcode.cn/problems/remove-element/>

题目描述：

给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并原地修改输入数组。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

示例 1: 给定 nums = [3,2,2,3], val = 3, 函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。 你不需要考虑数组中超出新长度后面的元素。

示例 2: 给定 nums = [0,1,2,2,3,0,4,2], val = 2, 函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。

你不需要考虑数组中超出新长度后面的元素。

解题：

1. 暴力求解：

注意，while是动态求解，每次循环都重新计算条件，for是静态求解

```
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i=0
        while i<len(nums):
            if nums[i] == val:
                for k in range(i+1,len(nums)):
                    nums[k-1]=nums[k]
                nums.pop()
            else:
                i+=1
        return len(nums)
```
注意随着数组每次移除元素，数组长度也会发生变化，所以需要用while语句

2. 双指针法（快慢指针法）： 通过一个快指针和慢指针在一个for循环下完成两个for循环的工作。

定义快慢指针

* 快指针：寻找新数组的元素 ，新数组就是不含有目标元素的数组
* 慢指针：指向更新 新数组下标的位置

慢指针收集的值就是最终数组，快指针往前探，发现可以留下的就给满指针。

```
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        slow=0
        fast=0
        l=len(nums)
        while fast<l:
            if nums[fast]!=val:
                nums[slow]=nums[fast]
                slow+=1
            fast+=1
        return slow
```
快指针跑得快，慢指针只会在收到好块时才前进。

