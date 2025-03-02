# [1893. 检查是否区域内所有整数都被覆盖](https://leetcode-cn.com/problems/check-if-all-the-integers-in-a-range-are-covered)

[English Version](/solution/1800-1899/1893.Check%20if%20All%20the%20Integers%20in%20a%20Range%20Are%20Covered/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>给你一个二维整数数组 <code>ranges</code> 和两个整数 <code>left</code> 和 <code>right</code> 。每个 <code>ranges[i] = [start<sub>i</sub>, end<sub>i</sub>]</code> 表示一个从 <code>start<sub>i</sub></code> 到 <code>end<sub>i</sub></code> 的 <strong>闭区间</strong> 。</p>

<p>如果闭区间 <code>[left, right]</code> 内每个整数都被 <code>ranges</code> 中 <strong>至少一个</strong> 区间覆盖，那么请你返回 <code>true</code> ，否则返回 <code>false</code> 。</p>

<p>已知区间 <code>ranges[i] = [start<sub>i</sub>, end<sub>i</sub>]</code> ，如果整数 <code>x</code> 满足 <code>start<sub>i</sub> <= x <= end<sub>i</sub></code> ，那么我们称整数<code>x</code> 被覆盖了。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<b>输入：</b>ranges = [[1,2],[3,4],[5,6]], left = 2, right = 5
<b>输出：</b>true
<b>解释：</b>2 到 5 的每个整数都被覆盖了：
- 2 被第一个区间覆盖。
- 3 和 4 被第二个区间覆盖。
- 5 被第三个区间覆盖。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<b>输入：</b>ranges = [[1,10],[10,20]], left = 21, right = 21
<b>输出：</b>false
<b>解释：</b>21 没有被任何一个区间覆盖。
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= ranges.length <= 50</code></li>
	<li><code>1 <= start<sub>i</sub> <= end<sub>i</sub> <= 50</code></li>
	<li><code>1 <= left <= right <= 50</code></li>
</ul>


## 解法

<!-- 这里可写通用的实现逻辑 -->

利用差分数组进行区间更新

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class Solution:
    def isCovered(self, ranges: List[List[int]], left: int, right: int) -> bool:
        diff = [0 for i in range(52)]
        for rg in ranges:
            diff[rg[0]] += 1
            diff[rg[1] + 1] -= 1
        cur = 0
        for i, df in enumerate(diff):
            cur += df
            if left <= i <= right and cur == 0:
                return False
        return True
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
class Solution {
    public boolean isCovered(int[][] ranges, int left, int right) {
        int[] diff = new int[52];
        for (int[] range : ranges) {
            diff[range[0]]++;
            diff[range[1] + 1]--;
        }
        int cur = 0;
        for (int i = 0; i < 52; i++) {
            cur += diff[i];
            if (left <= i && i <= right && cur == 0) {
                return false;
            }
        }
        return true;
    }
}
```

### **Go**

```go
func isCovered(ranges [][]int, left int, right int) bool {
	diff := make([]int, 52)
	for _, rg := range ranges {
		diff[rg[0]]++
		diff[rg[1]+1]--
	}
	cur := 0
	for i, df := range diff {
		cur += df
		if i >= left && i <= right && cur == 0 {
			return false
		}
	}
	return true
}
```

### **...**

```

```

<!-- tabs:end -->
