# **week 10**

*美好的一周从敲代码开始*

![image-20230712104538447](C:\Users\86152\AppData\Roaming\Typora\typora-user-images\image-20230712104538447.png)

[toc]

## 知识点记录：

### 位异或运算（XOR）

是一种逻辑运算符，用于比较两个二进制数的对应位，并根据以下规则计算结果：

- 如果对应位上的两个二进制数相同（都为0或都为1），则结果为0。
- 如果对应位上的两个二进制数不同（一个为0，一个为1），则结果为1。

位异或运算可以用符号 "^" 表示。

以下是一些位异或运算的示例：

```python
a = 10  # 二进制表示为 1010
b = 6   # 二进制表示为 0110

# 位异或运算
result = a ^ b  # 二进制表示为 1100，十进制为 12
print(result)  # 输出结果为 12
```

在上述示例中，变量 `a` 和 `b` 进行位异或运算，结果为 12。

位异或运算在计算机科学中有多种应用，包括：

- 交换两个变量的值：`a ^= b; b ^= a; a ^= b;`
- 判断两个数是否相等：`result = (a ^ b) == 0`
- 加密和解密算法中的数据处理
- 校验和和错误检测等领域

位异或运算是一种常用的位运算，可以在处理二进制数据和逻辑运算中发挥重要作用。

### 可哈希计数`collections.Counter`

`collections.Counter` 是 Python 标准库中的一个内置类，用于计数可哈希对象的出现次数。它提供了一种方便的方式来统计可迭代对象中各个元素的频率。

使用 `collections.Counter` 类可以快速统计可迭代对象中元素的出现次数，并以字典的形式返回统计结果，其中元素作为键，出现次数作为值。该类提供了一些实用的方法，可以进行计数的合并、计数器的相减、获取最常见的元素等操作。

以下是使用 `collections.Counter` 的示例：

```python
from collections import Counter

# 统计字符串中字符的出现次数
s = "hello world"
counter = Counter(s)
print(counter)  # 输出：Counter({'l': 3, 'o': 2, 'h': 1, 'e': 1, ' ': 1, 'w': 1, 'r': 1, 'd': 1})

# 统计列表中元素的出现次数
nums = [1, 2, 3, 1, 2, 3, 4, 5]
counter = Counter(nums)
print(counter)  # 输出：Counter({1: 2, 2: 2, 3: 2, 4: 1, 5: 1})

# 访问出现次数最多的元素
most_common = counter.most_common(2)
print(most_common)  # 输出：[(1, 2), (2, 2)]
```

在上述示例中，我们通过创建 `Counter` 对象并传入可迭代对象，可以快速统计元素的出现次数。通过调用 `most_common()` 方法，可以获取出现次数最多的元素及其对应的次数。

`collections.Counter` 是一个非常有用的工具，可以方便地进行频率统计和元素计数的操作，适用于许多数据处理和算法问题。

### 字母之间进行运算：

在 Python 中，可以使用内置的 `ord()` 和 `chr()` 函数将字母与 ASCII 码进行转换。通过将字母转换为 ASCII 码，可以进行一些运算操作。

下面是一些示例操作：

```python
# 字母向后移动 n 个位置
char = 'A'
n = 3
new_char = chr(ord(char) + n)
print(new_char)  # 输出：D

# 字母向前移动 n 个位置
char = 'D'
n = 3
new_char = chr(ord(char) - n)
print(new_char)  # 输出：A

# 字母间的差值
char1 = 'E'
char2 = 'B'
diff = ord(char1) - ord(char2)
print(diff)  # 输出：3
```

通过对字母的 ASCII 码进行加减操作，可以实现字母的移动或计算字母之间的差值。注意要确保结果仍然是合法的字母。

### 内置函数`bisect_right`右二等分

`bisect_right`是 Python 中模块的函数`bisect`。它用于在排序列表中查找目标值的插入点。

以下是如何使用的示例`bisect_right`：

```python
from bisect import bisect_right

nums = [1, 3, 5, 7, 9]
target = 4

idx = bisect_right(nums, target)
print(idx)  # Output: 2
```

在此示例中，`bisect_right(nums, target)`返回应插入的索引`target`以维护 list 的排序顺序`nums`。由于`target`是 4 并且它应该插入到列表中的值 3 之后，因此返回的索引是 2。

在代码上下文中，您可以使用`bisect_right`来查找目标字母应插入到字母排序列表中的索引。



## [39. 组合总和](https://leetcode.cn/problems/combination-sum/)

### 题目描述：

给你一个 **无重复元素** 的整数数组 `candidates` 和一个目标整数 `target` ，找出 `candidates` 中可以使数字和为目标数 `target` 的 所有 **不同组合** ，并以列表形式返回。你可以按 **任意顺序** 返回这些组合。

`candidates` 中的 **同一个** 数字可以 **无限制重复被选取** 。如果至少一个数字的被选数量不同，则两种组合是不同的。 

对于给定的输入，保证和为 `target` 的不同组合数少于 `150` 个。

```python
```



### 解题思路：



## [122. 买卖股票的最佳时机 II](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)

### 题目描述：

给你一个整数数组 `prices` ，其中 `prices[i]` 表示某支股票第 `i` 天的价格。

在每一天，你可以决定是否购买和/或出售股票。你在任何时候 **最多** 只能持有 **一股** 股票。你也可以先购买，然后在 **同一天** 出售。

返回 *你能获得的 **最大** 利润* 。

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        n = len(prices)  # 股票价格的天数
        res = 0  # 最大利润初始化为0
        for i in range(1, n):  # 遍历股票价格列表
            if prices[i] > prices[i-1]:  # 如果当天的股票价格高于前一天的价格
                res += prices[i] - prices[i-1]  # 将差值加到最大利润上
        return res
```



### 解题思路：

贪心算法：在每个阶段选择局部最优解以期望最终获得全局最优解

通过比较相邻两天的股票价格来判断是否进行买卖操作，并将利润累加到最大利润中。由于可以多次买卖股票，我们可以在价格上升的时候买入，价格下降的时候卖出，这样可以获得最大利润。股票总交易可以看作数次小交易的和。



## [1911. 最大子序列交替和](https://leetcode.cn/problems/maximum-alternating-subsequence-sum/)

### 题目描述：

一个下标从 **0** 开始的数组的 **交替和** 定义为 **偶数** 下标处元素之 **和** 减去 **奇数** 下标处元素之 **和** 。

- 比方说，数组 `[4,2,5,3]` 的交替和为 `(4 + 5) - (2 + 3) = 4` 。

给你一个数组 `nums` ，请你返回 `nums` 中任意子序列的 **最大交替和** （子序列的下标 **重新** 从 0 开始编号）。

一个数组的 **子序列** 是从原数组中删除一些元素后（也可能一个也不删除）剩余元素不改变顺序组成的数组。比方说，`[2,7,4]` 是 `[4,**2**,3,**7**,2,1,**4**]` 的一个子序列（加粗元素），但是 `[2,4,2]` 不是。

```python
```



### 解题思路：



## 每日一题：

### [2544. 交替数字和](https://leetcode.cn/problems/alternating-digit-sum/) ——难度简单

#### 题目描述：

给你一个正整数 `n` 。`n` 中的每一位数字都会按下述规则分配一个符号：

- **最高有效位** 上的数字分配到 **正** 号。
- 剩余每位上数字的符号都与其相邻数字相反。

返回所有数字及其对应符号的和。

```python
class Solution:
    def alternateDigitSum(self, n: int) -> int:
        res = 0
        sign = 1
        while n:
            res += (n % 10) * sign
            n //= 10
            sign = -sign
        return res * -sign
```

#### 解题思路：

**示例 3：**

```
输入：n = 886996
输出：0
解释：(+8) + (-8) + (+6) + (-9) + (+9) + (-6) = 0
```

从事例可以得出，从最后一位开始遍历，`sign = 1`，循环结束时，

- `len(n)`如果是偶数，`sign = -1`, 结果`res * -sign` = `res`
- `len(n)`如果是奇数，`sign = 1`, 结果`res * -sign` = `-res`，就是说起始位置是`n`的末尾应该是`sign = -1`

### [931. 下降路径最小和](https://leetcode.cn/problems/minimum-falling-path-sum/)——难度中等

#### 题目描述：

给你一个 `n x n` 的 **方形** 整数数组 `matrix` ，请你找出并返回通过 `matrix` 的**下降路径** 的 **最小和** 。

**下降路径** 可以从第一行中的任何元素开始，并从每一行中选择一个元素。在下一行选择的元素和当前行所选元素最多相隔一列（即位于正下方或者沿对角线向左或者向右的第一个元素）。具体来说，位置 `(row, col)` 的下一个元素应当是 `(row + 1, col - 1)`、`(row + 1, col)` 或者 `(row + 1, col + 1)` 。

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/11/03/failing1-grid.jpg)

```
输入：matrix = [[2,1,3],[6,5,4],[7,8,9]]
输出：13
解释：如图所示，为和最小的两条下降路径
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/11/03/failing2-grid.jpg)

```
输入：matrix = [[-19,57],[-40,-5]]
输出：-59
解释：如图所示，为和最小的下降路径
```

```python
class Solution:
    def minFallingPathSum(self, matrix: List[List[int]]) -> int:
        n = len(matrix)  # 矩阵的大小
        dp = [[0] * n for _ in range(n)]  # dp数组
        dp[0] = matrix[0]  # 初始化dp数组
        
        for i in range(1, n):
            for j in range(n):
                # 计算当前位置的最小路径和
                if j == 0:  # 左边界
                    dp[i][j] = matrix[i][j] + min(dp[i-1][j], dp[i-1][j+1])
                elif j == n - 1:  # 右边界
                    dp[i][j] = matrix[i][j] + min(dp[i-1][j], dp[i-1][j-1])
                else:  # 正常情况
                    dp[i][j] = matrix[i][j] + min(dp[i-1][j], dp[i-1][j-1], dp[i-1][j+1])
        
        return min(dp[n-1])
```



#### 解题思路：

最开始想的是贪心算法，第一行的最小的位置 `(row, col)` 的，加上第二行的 `(row + 1, col - 1)`、`(row + 1, col)` 或者 `(row + 1, col + 1)` 最小的一个，只通过一般的测试点，然后改用`动规`的方法，每一行都需要找到最小数的合并结果，输出`dp数组`最后一行的的最小值就是我们要的答案。注意：`python数组`对边界溢出较为敏感，要考虑到边界也就是特殊情况的处理。
