## **68. Text Justification**

[LeetCode 68. Text Justification [Hard]](https://leetcode.com/problems/text-justification/description/)

Given an array of strings `words` and a width `maxWidth`, format the text such that each line has exactly `maxWidth` characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces `' '` when necessary so that each line has exactly `maxWidth` characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified, and no extra space is inserted between words.

**Note:**

* A word is defined as a character sequence consisting of non-space characters only.
* Each word's length is guaranteed to be greater than `0` and not exceed `maxWidth`.
* The input array `words` contains at least one word.

```markdown
Input: words = ["This", "is", "an", "example", "of", "text", "justification."], maxWidth = 16
Output:
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
```

```markdown
Input: words = ["What","must","be","acknowledgment","shall","be"], maxWidth = 16
Output:
[
  "What   must   be",
  "acknowledgment  ",
  "shall be        "
]
Explanation: Note that the last line is "shall be    " instead of "shall     be", because the last line must be left-justified instead of fully-justified.
Note that the second line is also left-justified because it contains only one word.
```

### **思路**
* **从头开始记录字符串的长度 当加上当前词语字符串长度大于 `maxWidth`时 进行 `reconstruct` 将重组后的字符串加入 `res` 中 当过完全部词语后 检查最后一行 因为最后一行的结算方式和之前不同 将最后一行调整完成后 得出最后结果**
* **reconstruct 过程中 先检查输入的总词数 若为 `1` 则直接插入 `" "` 导出 其他情况则先利用 `.join()` 在词语间插入 `" "` 并得出完整字符串 之后按照顺序查找字符串中 前一个字符为英文字母 后一个字符为 `" "` 的情况 并在英文字母后添加 `" "`**
* **注意：因为在添加括号的过程中字符串的长度发生变化 所以不能通过 `for(i in range(len(n)))` 来循环 必须及时更新长度 否则可能产生末尾无法更新的情况**
* **在作最后一行调整的过程中用到了 `.split()` 如果括号内不填信息 则将一句话中的空格全部舍去 只留下单词 依次存储在 `list` 中 也可使用 `.split(" ")` 等按照需求进行分割**

### **代码**

``` python
class Solution:
    def fullJustify(self, words: List[str], maxWidth: int) -> List[str]:
        res = []
        count_list, curr_len = [], 0

        for i in range(len(words)):
            if curr_len + len(words[i]) > maxWidth:
                self.reconstruct(count_list, res, maxWidth)
                count_list, curr_len = [], 0
            count_list.append(words[i])
            curr_len = curr_len + len(words[i]) + 1

        if count_list:
            temp_list = " ".join(count_list)
            res.append(temp_list + " " * (maxWidth - len(temp_list)))
        else:
            count_list = res[-1].split()
            temp_list = " ".join(count_list)
            res[-1] = (temp_list + " " * (maxWidth - len(temp_list)))

        return res

    def reconstruct(self, count_list, res, maxWidth):
        if len(count_list) == 1:
            res.append(count_list[0] + " " * (maxWidth - len(count_list[0])))
            return None
        else:
            temp_list = " ".join(count_list)
            while(True):
                length, i = len(temp_list), 0
                while(length > 0):
                    if len(temp_list) == maxWidth:
                        res.append(temp_list)
                        return None
                    if temp_list[i] == " " and temp_list[i - 1] != " ":
                        temp_list = temp_list[:i] + "  " + temp_list[i+1:]
                        length += 1
                    length -= 1
                    i += 1


```
### **复杂度分析**
* **时间复杂度：O(n)**
* **空间复杂度：O(n)**
