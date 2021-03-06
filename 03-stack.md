# 某关于字符串匹配的问题

## 问题

有两个人分别叫 K 和 J，他们是棋逢对手的宿敌。由于 K 的地位比 J 高，所以每次对决时必须由 K 先出招，J 为了表示对 K 的尊敬，也会回敬相同次数的出招。但在一次对决中，发生了时空错乱，导致两人出招的顺序发生了改变。现在你有修正时空的能力，可以将两人出招的顺序修正过来。请找出最小需要改变时空的次数。

### 样例

样例1：

input1: JK

output1: 2

> 说明：由于 K 必须先出招，所以第一个 J 要改成 K，而 J 必须回敬一次 K 的出招，所以第二个 K 要改成 J，总共需要修改 2 次。

样例2：

input1: KKKK

output2: 2

> 说明：由于 J 的出手次数必须和 K 相同，所以将第二、第四个位置的 K 改为 J，一共需要修改 2 次。

## 题解

本题难度：🌕🌕

本题不要被这个背景唬住。本质上是字符串配对的问题。进一步抽象，可以将 J 看成右括号，K 看成左括号。实际上就变成了括号配对。根据题目的要求，两个成对的括号必须配对，那么剩下的就是需要修改的。

这里可以建立一个栈，分为下列情况：

1. 栈空，无论压入什么都必须压入。
2. 栈非空，且栈顶元素为 K，当试图压入 J 时，弹出栈顶。
3. 栈非空，且栈顶元素为 K，当试图压入 K 时，压入。
4. 栈非空，且栈顶元素为 J，无论压入什么都必须压入。

当遍历完输入字符串后，栈内剩下的元素：

1. 若为奇数，则不可能有符合要求的解，输出 -1。
2. 若为偶数，则建立一个和栈等长的字符串，其中为 K、J、K、J……的交替序列。
3. 栈（此时不再看成栈）和字符串比较，若不一样则记录一次变换。

## 代码

```python
def solve3(input1: str) -> int:
    stack = []
    ex = 0
    for ch in input1:
        if not stack:
            stack.append(ch)
        elif stack[-1] == 'K':
            if ch == 'J':
                stack.pop()
            elif ch == 'K':
                stack.append(ch)
        elif stack[-1] == 'J':
            stack.append(ch)
    if len(stack) % 2 != 0:
        return -1
    else:
        s = ''
        for i in range(len(stack)):
            if i % 2 == 0:
                s += 'K'
            else:
                s += 'J'
        for i in range(len(stack)):
            if stack[i] != s[i]:
                ex += 1
        return ex
```

只可惜这个题没做完，被样例坑了，以为 J 和 K 一定是交替序列，调试调了很久，到最后时间来不及了。但我觉得我的解法应该是对的。
