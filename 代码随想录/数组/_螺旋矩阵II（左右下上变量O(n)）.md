
<https://leetcode.cn/problems/spiral-matrix-ii/>

题目描述：

给定一个正整数 n，生成一个包含 1 到 n^2 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。

示例:

![](./attachments/_螺旋矩阵II（左右下上变量O(n)）_001.png)

输入: 3 输出: [ [ 1, 2, 3 ], [ 8, 9, 4 ], [ 7, 6, 5 ] ]

解题：

生成螺旋矩阵的本质是**模拟顺时针填充过程**。我们可以定义四个边界：

* `top`：上边界（行索引，初始 0）
* `bottom`：下边界（行索引，初始 n-1）
* `left`：左边界（列索引，初始 0）
* `right`：右边界（列索引，初始 n-1）

然后按照 **左→右、上→下、右→左、下→上** 的顺序依次填充数字，每填充完一行或一列，就收缩对应的边界，直到所有数字填完。

```
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        re = [[0]*n for _ in range(n)]
        nums=0
        top=0
        bottom=n-1
        left=0
        right=n-1
        while nums<n*n:
            for i in range(left,right+1):
                nums+=1
                re[top][i]=nums
            top+=1
            for j in range(top,bottom+1):
                nums+=1
                re[j][right]=nums
            right-=1
            for k in range(right,left-1,-1):
                nums+=1
                re[bottom][k]=nums
            bottom-=1
            for h in range(bottom,top-1,-1):
                nums+=1
                re[h][left]=nums
            left+=1
        return re
```
注意边界，最左最右最上最下都要取到

