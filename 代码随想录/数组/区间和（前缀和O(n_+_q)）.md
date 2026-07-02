<https://kamacoder.com/problempage.php?pid=1070>

题目描述：

给定一个整数数组 Array，请计算该数组在每个指定区间内元素的总和。

输入描述

第一行输入为整数数组 Array 的长度 n，接下来 n 行，每行一个整数，表示数组的元素。随后的输入为需要计算总和的区间，直至文件结束。

输出描述

输出每个指定区间内元素的总和。

输入示例

```
5
1
2
3
4
5
0 1
1 3
```
输出示例

```
3
9
```
数据范围：

0 < n <= 100000

解题思路：

1. 暴力求解易超时，因为暴力求解每次区间和要重复计算
2. 前缀和，即前面几个值的和算出，每次求区间和只要将前缀和相减，闭区间
3. `sys.stdin.read().split()` 一次性读取所有数字，然后按顺序解析

sys.stdin 代表标准输入流，是一个文件对象

.read() 是文件对象的读取方法，一次性读取所有输入，直到EOF，返回一个大的字符串

.split() 按默认任意空白字符分割，返回一个列表

```
import sys
data = sys.stdin.read().split()
def main():
    if not data:
        return
    n = int(data[0])
    index=1
    vec=[]

    #将字符串列表转换成整数数组
    for i in range(n):
        vec.append(int(data[i+index]))
    index+=n

    #构造前缀和数组
    p=[0]*n
    count=0
    for i in range(n):
        count+=vec[i]
        p[i]=count

    result=[]
    while index<len(data):
        left = int(data[index])
        right = int(data[index+1])
        index+=2
        #边界维护
        if left==0:
            sum_v=p[right]
        else:
            sum_v=p[right]-p[left-1]
        print(sum_v)

if __name__ =="__main__":
    main()
```
注意：index是为了记录处理过的数的个数防止忘记

边界维护牢记

