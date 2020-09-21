# 某关于等差数列的问题

## 问题

已知一数列 $\{a_n\}$, 其首项 $a_0$ 和末项 $a_n$ 的和与第二项 $a_1$ 和 倒数第二项 $a_{n-1}$ 的和相等，以此类推。且该数列单调递增。现在这一数列丢失了一个数 $a_x$（该数不在头尾），求该数。

### 样例

样例1：

input1: 5
input2: {1, 3, 5, 9, 11}

output1: 7

样例2：

input1: 5
input2: {2, 4, 6, 10, 12}

output2: 8

## 题解

本题难度：🌕

本题非常简单，给了很多有利条件（如首尾元素存在，数列单调递增）。因此只要先计算首尾元素的和，再从第二个元素开始遍历，至多只要遍历原数组的一半即可找到缺失的数。时间复杂度为 $O(n)$.

## 代码

```python
def solve1(input1:int, input2: list[int]) -> int:
    s = input2[0] + input2[input1 - 1]
    for i in range(1, input1):
        if s - input2[i] not in input2: # Python 的 not in 真是太方便了
            return s - input2[i]
```

