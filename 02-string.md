# 某关于字符串的问题

## 问题

给定一段文本 `text`，由若干单词组成，单词之间由空格分隔。现在这个文本中的每个单词都被人打乱了，打乱的方式是从左往右循环移位 $K$ 次。但即使这样，文本中仍有一些单词没有发生变化，请找出没有发生变化的单词的个数。

### 样例

样例1：

input1: "llohe ereth"
input2: 2

output1: 0

> 说明：原单词是 "hello there", 经过 2 次变换后，变换后的单词和原单词不相等，因此输出 0.

样例2：

input1: "adaada"
input2: 3

output2: 1

> 说明：原单词是 "adaada"，变换 3 次以后和原单词相等，于是输出 1.

## 题解

本题难度：🌕🌗

首先分割该字符串，得到每个单词的序列。对每个单词，进行循环移位，若移位后的单词和原单词相等，则相等的单词数+1.

**此处有坑：要考虑单词变换次数大于（甚至远大于）单词本身长度的问题。** 如果真的采用机械式的循环移位，真的遇到变换次数远大于单词本身长度的时候，可能会超时。（感谢出题人没有出这么变态的样例）

## 代码

```python
def solve2(input1: str, input2: int)->int:
    all_words = input1.split()
    num_of_correct_words = 0
    for word in all_words:
        r = input2 % len(word)
        new_word = word[r:] + word[:r]  # Python 的切片操作真是太方便啦
        if new_word == word:
            num_of_correct_words += 1
    return num_of_correct_words
```