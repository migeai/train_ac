# **week 9**

## [29. 两数相除](https://leetcode.cn/problems/divide-two-integers/)

### 题目描述：

给你两个整数，被除数 `dividend` 和除数 `divisor`。将两数相除，要求 **不使用** 乘法、除法和取余运算。

整数除法应该向零截断，也就是截去（`truncate`）其小数部分。例如，`8.345` 将被截断为 `8` ，`-2.7335` 将被截断至 `-2` 。

返回被除数 `dividend` 除以除数 `divisor` 得到的 **商** 。

**注意：**假设我们的环境只能存储 **32 位** 有符号整数，其数值范围是 [$−2^{31}$, $2^{31}$ − 1] 。本题中，如果商 **严格大于** $2^{31}$  − 1，则返回 $2^{31}$  − 1 ；如果商 **严格小于**$-2^{31}$  ，则返回 $-2^{31}$  。

```python
class Solution:
    def divide(self, dividend: int, divisor: int) -> int:
        if dividend == 0:  # 处理特殊情况，被除数为0
            return 0
        if divisor == 1:  # 特殊情况处理，除数为1，直接返回被除数
            return dividend
        if divisor == -1:  # 特殊情况处理，除数为-1
            if dividend > -2 ** 31:  # 只要不是最小的负数，直接返回被除数的相反数
                return -dividend
            return 2 ** 31 - 1  # 是最小的负数，返回最大的整数
        a, b = abs(dividend), abs(divisor)  # 取绝对值
        sign = 1  # 符号，默认为正
        if (divisor > 0 and dividend < 0) or (divisor < 0 and dividend > 0):
            sign = -1  # 如果除数和被除数符号不同，则结果为负数
        res = self.div(a, b)  # 调用递归函数进行除法运算
        if sign > 0:
            return min(res, 2 ** 31 - 1)  # 如果结果为正数，返回结果和最大整数中较小的那个
        return max(-res, -2 ** 31)  # 如果结果为负数，返回结果的相反数

    def div(self, a: int, b: int) -> int:
        if a < b:
            return 0
        count = 1
        tb = b
        while (tb + tb) <= a:
            count += count  # 最小解翻倍
            tb += tb  # 当前测试的值也翻倍
        return count + self.div(a - tb, b)

```

### 解题思路：

题目要求使用加减法拟合整除运算，先考虑一些特殊情况，接着具体算法实现，定义一个类内函数

功能实现：

- 类似进制的计算，像60/8 = （32 + 16 + 8）/ 8 = 4 + 2 + 1 = 8



## [31. 下一个排列](https://leetcode.cn/problems/next-permutation/)

### 题目描述：

整数数组的一个 **排列** 就是将其所有成员以序列或线性顺序排列。

- 例如，`arr = [1,2,3]` ，以下这些都可以视作 `arr` 的排列：`[1,2,3]`、`[1,3,2]`、`[3,1,2]`、`[2,3,1]` 。

整数数组的 **下一个排列** 是指其整数的下一个字典序更大的排列。更正式地，如果数组的所有排列根据其字典顺序从小到大排列在一个容器中，那么数组的 **下一个排列** 就是在这个有序容器中排在它后面的那个排列。如果不存在下一个更大的排列，那么这个数组必须重排为字典序最小的排列（即，其元素按升序排列）。

- 例如，`arr = [1,2,3]` 的下一个排列是 `[1,3,2]` 。
- 类似地，`arr = [2,3,1]` 的下一个排列是 `[3,1,2]` 。
- 而 `arr = [3,2,1]` 的下一个排列是 `[1,2,3]` ，因为 `[3,2,1]` 不存在一个字典序更大的排列。

给你一个整数数组 `nums` ，找出 `nums` 的下一个排列。

必须**[ 原地 ](https://baike.baidu.com/item/原地算法)**修改，只允许使用额外常数空间。

```python
class Solution:
    def nextPermutation(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        if n <= 1:   # 如果长度为一，不用进行任何操作，直接返回
            return 
        # 找到从右到左的第一个递减的元素。
        i = n - 2
        while i >= 0 and nums[i] >= nums[i+1]:
            i -= 1
        # 找到要交换的数
        if i >= 0:
            j = n - 1
            while j > i and nums[j] <= nums[i]:  # 从右向左找到第一个大于 nums[i] 的数
                j -= 1
            nums[i], nums[j] = nums[j], nums[i]  # 交换两个数的位置
        # nums[i+1:]要递减排列，保证是以 nums[:i+1] 为前缀的最小排列
        nums[i+1:] = nums[i+1:][::-1]  # 将 nums[i+1:] 反转，使其递增排列

```

### 解题思路：

是 次最大字典序排列问题

从右向左找到第一个降序序的位置，从右向左找到第一个大于其的数，交换两个数的位置，剩下的要递增排列

1 2 4 5 3 -> 找到 2==i, j == 3（下标） 交换 1 2 5 4 3   nums[i+1:]要递减排列要递减排列 -> 1 2 5 4 3 

## [33. 搜索旋转排序数组](https://leetcode.cn/problems/search-in-rotated-sorted-array/)

### 题目描述：

整数数组 `nums` 按升序排列，数组中的值 **互不相同** 。

在传递给函数之前，`nums` 在预先未知的某个下标 `k`（`0 <= k < nums.length`）上进行了 **旋转**，使数组变为 `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]`（下标 **从 0 开始** 计数）。例如， `[0,1,2,4,5,6,7]` 在下标 `3` 处经旋转后可能变为 `[4,5,6,7,0,1,2]` 。

给你 **旋转后** 的数组 `nums` 和一个整数 `target` ，如果 `nums` 中存在这个目标值 `target` ，则返回它的下标，否则返回 `-1` 。

你必须设计一个时间复杂度为 `O(log n)` 的算法解决此问题。

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        n = len(nums)
        l, r = 0, n - 1
        while l <= r:
            mid = l + (r - l) // 2  # 计算中间位置
            if nums[mid] == target:
                return mid
            
            if target >= nums[0]:  # 如果目标值大于等于数组第一个元素
                if nums[mid] > target or nums[mid] < nums[0]:
                    r = mid - 1  # 目标值在左半边，更新右边界
                else:
                    l = mid + 1  # 目标值在右半边，更新左边界
            else:  # 如果目标值小于数组第一个元素
                if target > nums[mid] or nums[mid] >= nums[0]:  # 包括可能相等的情况
                    l = mid + 1  # 目标值在右半边，更新左边界
                else:
                    r = mid - 1  # 目标值在左半边，更新右边界
        return -1  # 未找到目标值

    
# 简单的话就是
for i in nums:  # for i in range(len(nums))也是可以的
    if i == target:
        return nums.index(i)
return -1
```



### 解题思路：

本题求出结果还是比较简单的，但搜索算法是要求利用较少的时间例如二分完成$O(n) \longrightarrow O(log(n))$

考虑到数组结构是一部分递减，一部分递增，当目标值大于第一个值,，中间值大于目标值*(若存在就在中间小于，后面一段是小于它的例如4 5 6 0 1 2，target= 5 ，0 1 2一定小于目标值，如果mid的值是$0<4$,target 位于（0~mid）)*，或则中间值小于第一个值都是在左边.

### 注意：

详细跳转到$\longrightarrow$[ACM 选手带你玩转二分查找！](https://mp.weixin.qq.com/s?__biz=MzI0NjAxMDU5NA==&mid=2475922852&idx=1&sn=f6990bcafef36c96599866ab99bb25f2&chksm=ff22f229c8557b3fab35b99c29038eb4ea0c024010128eb09e8923922666e16e3928b1ed4edf&scene=21#wechat_redirect)

***mid 取值**

mid 这个取值的话，一般不会有啥问题，基本都是下面这样：

```
 mid = (low + high) / 2
```

但是叭，我拿 Python 来说，Python 里整数值不受位数限制，正常来讲那就是它可以无限大，但是计算机毕竟有内存，你总得是有个限制。

加法这个叭，总归是不好控制，万一就有特别大的时候呢？

所以还是减起来舒服，所以碰到 low 或 high 特别大的时候，mid 可以取下面这样：

```
mid = low + (high - low) / 2
```



## [34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/)

### 题目描述：

给你一个按照非递减顺序排列的整数数组 `nums`，和一个目标值 `target`。请你找出给定目标值在数组中的开始位置和结束位置。

如果数组中不存在目标值 `target`，返回 `[-1, -1]`。

你必须设计并实现时间复杂度为 $O(log (n)$ 的算法解决此问题。

```python
class Solution:
    def searchleft(self, nums: List[int], target: int) -> int:
        n = len(nums)
        low, high = 0, n - 1  # 初始化左右指针
        while low <= high:
            mid = low + (high - low) // 2  # 计算中间位置
            if nums[mid] < target:
                low = mid + 1  # 目标值在右半边，更新左边界
            elif nums[mid] > target:
                high = mid - 1  # 目标值在左半边，更新右边界
            else:  # 相等时继续向左搜索，更新右边界
                high = mid - 1
        if nums[low] == target:  # 找到目标值
            return low
        else:  # 没找到
            return -1

    def searchright(self, nums: List[int], target: int) -> int:
        n = len(nums)
        low, high = 0, n - 1  # 初始化左右指针
        while low <= high:
            mid = low + (high - low) // 2  # 计算中间位置
            if nums[mid] < target:
                low = mid + 1  # 目标值在右半边，更新左边界
            elif nums[mid] > target:
                high = mid - 1  # 目标值在左半边，更新右边界
            else:  # 相等时继续向右搜索，更新左边界
                low = mid + 1
        if nums[high] == target:  # 找到目标值
            return high
        else:  # 没找到
            return -1

    def searchRange(self, nums: List[int], target: int) -> List[int]:
        if  len(nums) == 0 or nums[-1] < target or nums[0] > target:  # 特殊条件，目标值不在数组范围内或数组为空
            return [-1, -1]
        lm = self.searchleft(nums, target)  # 搜索左边界
        if lm == -1:
            rm = -1  # 左边界不存在，右边界也不存在
        else:
            rm = self.searchright(nums, target)  # 搜索右边界

        return [lm, rm]  # 返回左右边界结果
```



### 解题思路：

二分查找算法，注意第35行代码，$len(nums) == 0$  要写在前面，因为避免**IndexError: list index out of range**。

## [36. 有效的数独](https://leetcode.cn/problems/valid-sudoku/)

### 题目描述：

请你判断一个 `9 x 9` 的数独是否有效。只需要 **根据以下规则** ，验证已经填入的数字是否有效即可。

1. 数字 `1-9` 在每一行只能出现一次。
2. 数字 `1-9` 在每一列只能出现一次。
3. 数字 `1-9` 在每一个以粗实线分隔的 `3x3` 宫内只能出现一次。（请参考示例图）

**注意：**

- 一个有效的数独（部分已被填充）不一定是可解的。
- 只需要根据以上规则，验证已经填入的数字是否有效即可。
- 空白格用 `'.'` 表示。

 ```python
 class Solution:
     def isValidSudoku(self, board: List[List[str]]) -> bool:
         rows = [[0] * 9 for i in range(9)]  # 每行数字的计数器
         columns = [[0] * 9 for i in range(9)]  # 每列数字的计数器
         cells = [[0] * 9 for i in range(9)]  # 每个小九宫格数字的计数器
 
         for i in range(9):
             for j in range(9):
                 if board[i][j] != '.':
                     num = int(board[i][j]) - 1  # 将字符转换为数字，范围为0-8
                     box_index = (i//3) * 3 + j // 3  # 计算小九宫格的索引
                     
                     # 更新计数器
                     rows[i][num] += 1
                     columns[j][num] += 1
                     cells[box_index][num] += 1
 
                     # 检查当前数字在行、列、小九宫格中是否重复出现
                     if  rows[i][num] > 1 or columns[j][num] > 1 or cells[box_index][num] > 1:
                         return False
         return True
 ```

### 解题思路：

开始是遍历了两遍整个数组，时间和空间都比较大，后来看了一下官方的题解是可以只用遍历一遍，自己又修改了一下，思路还是用数组记录行、列、小宫格中的数，而后判断是否重复。

```css
box_index = (i//3) * 3 + j // 3  # 计算小九宫格的索引 九个小宫格 
```

$(0, 3) * 3 + (0, 3) = (0, 9) $ 由数组储存形式 $[3 * 3 * 9] \longrightarrow [9 * 9]$。

- 注意：python的bool形式是True 和 False

## [38. 外观数列](https://leetcode.cn/problems/count-and-say/)

### 题目描述：

给定一个正整数 `n` ，输出外观数列的第 `n` 项。

「外观数列」是一个整数序列，从数字 1 开始，序列中的每一项都是对前一项的描述。

你可以将其视作是由递归公式定义的数字字符串序列：

- `countAndSay(1) = "1"`
- `countAndSay(n)` 是对 `countAndSay(n-1)` 的描述，然后转换成另一个数字字符串。

前五项如下：

```
1.     1
2.     11
3.     21
4.     1211
5.     111221
第一项是数字 1 
描述前一项，这个数是 1 即 “ 一 个 1 ”，记作 "11"
描述前一项，这个数是 11 即 “ 二 个 1 ” ，记作 "21"
描述前一项，这个数是 21 即 “ 一 个 2 + 一 个 1 ” ，记作 "1211"
描述前一项，这个数是 1211 即 “ 一 个 1 + 一 个 2 + 二 个 1 ” ，记作 "111221"
```

要 **描述** 一个数字字符串，首先要将字符串分割为 **最小** 数量的组，每个组都由连续的最多 **相同字符** 组成。然后对于每个组，先描述字符的数量，然后描述字符，形成一个描述组。要将描述转换为数字字符串，先将每组中的字符数量用数字替换，再将所有描述组连接起来。

例如，数字字符串 `"3322251"` 的描述如下图：

![img](https://pic.leetcode-cn.com/1629874763-TGmKUh-image.png)

```python
class Solution:
    def countAndSay(self, n: int) -> str:
        num_str = '1'
        if n == 1:  # 特殊处理
            return num_str

        while n > 1:
            new_str = ""
            count = 1
            for i in range(1, len(num_str)):
                if num_str[i] == num_str[i-1]:  # 如果当前字符与前一个字符相同
                    count += 1
                else:  # 如果当前字符与前一个字符不同
                    new_str += str(count) + num_str[i-1]  # 将前一个字符的计数和字符添加到new_str中
                    count = 1  # 重置计数器为1

            new_str += str(count) + num_str[-1]  # 添加最后一个字符的计数和字符到new_str中
            num_str = new_str  # 将new_str赋值给num_str，准备进行下一次迭代
            n -= 1

        return num_str
```



### 解题思路：

本题还是较为简单，常规思路，字符串处理，使用`new_str`记录外观数列的第 `n` 项，`new_str += str(count) + num_str[i-1]`注意这个只记录到`len(num_str) - 1 `， 所以要加上`new_str += str(count) + num_str[-1]`。



 
