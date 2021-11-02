---
layout:     post
title:      "leetcode＆OJ刷题记录"
subtitle:   ""
date:       2021-07-07 	12:48:08
author:     "xnchen"
header-img: "img/home-bg.jpg"
tags:
    - leetcode
    - 算法
    - Golang
---



### 标志注释

\* ：不会

? ：有点疑惑

√ ：过了

### 每日一题

| 序号题目                                                     | 类型           | 解法思路                                                     | 算法复杂度 | 结果 |
| ------------------------------------------------------------ | -------------- | ------------------------------------------------------------ | ---------- | ---- |
| [1711. 大餐计数](https://leetcode-cn.com/problems/count-good-meals/) | 双指针、哈希表 | 1. 数组内数大小在[min, max]范围内，则满足条件的2的幂次在[min, 2*max]中，这个复杂度为logC<br>2. 如果直接去找所有组合可能为2的幂次的数量，复杂度是O(n^2*logC)以上。应该首先将所有数出现的次数存到Dict中。（可以先sort，使顺序从小到大）。然后左右flag去查相加为某个2幂次的数（两数之和）（复杂度为N），进行logC次。 | O(NlogC)   | \*   |

### GO

| 题目序号                                                     | 类型   | 解法思路                                                     | 时间复杂度 |空间复杂度|结果|
| ------------------------------------------------------------ | ------ | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)     | 哈希表 | 1. go的字典写法：`goDict := make(map[int]int)`<br>    或者`goDict := map[int] int{}` <br>2. go的查询字典中键值是否存在的写法：`if _, ok := goDict[key]; ok {}`<br>3. go遍历list的写法：`for index, number := range nums {}` | O(logN)    |O(logN)|√|
| [剑指 Offer 56 - I. 数组中数字出现的次数](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/) | 位操作 | 1. go的转换二进制字符串方法：`fmt.Sprintf("%08b", number)`或者`strconv.FormatInt(number, 2)`<br>2. go的异或：a^b<br>3. go的字符转数字：`rune(c)`，数字转字符串：`string(num)` | O(logN)    |O(1)|？|
| [1832. 判断句子是否为全字母句](https://leetcode-cn.com/problems/check-if-the-sentence-is-pangram/) |  | 1. go创建固定长度列表的方法：`var l[26] int`<br>更新：这样在长度是var的时候会报错，请用`l=make([]int, length)`<br>2. go快速判断元素是否在数组中：[使用sort.SearchSrtings()](https://cloud.tencent.com/developer/article/1729114) 可将判断元素在数组中的问题降低复杂度到O(logN) |  ||√|
| [1833. 雪糕的最大数量](https://leetcode-cn.com/problems/maximum-ice-cream-bars/) | 哈希表 | 方法1：先排序，再计算，复杂度=排序的O(NlogN)<br>go的列表排序方法：`sort.Ints(targetList)`<br>方法2：因为雪糕的最大价格不超过1e5，使用列表记录每个价格的雪糕的数量。空间复杂度换时间复杂度。 | O(N+C)，C是雪糕最大价格 |O(C)|？|
| [1722. 执行交换操作后的最小汉明距离](https://leetcode-cn.com/problems/minimize-hamming-distance-after-swap-operations/) | 并查集、哈希表 | 1. 分析题目，如果[0,1],[1,2]可以交换，那么[0,2]也可以交换。因此所有可以交换的索引可以形成一个集合，其中两两可以交换<br>2. 使用并查集得到交换操作的集合<br>3. 对于每一个集合，使用哈希表记录集合内索引对应的目标数组数据出现的次数。对于输入数组的每一个数，找出其索引所在集合和目标数组集合的差集，就是结果。 | O(N+M)<br>N为集合长度，M为交换列表长度 ||\*|
| [930. 和相同的二元子数组](https://leetcode-cn.com/problems/binary-subarrays-with-sum/) | 哈希表法、三指针法 | 1. 哈希表法：用哈希表存储hash[sum]（从最左侧到index i的累计为sum的数量），在index i，查找hash[sum-goal]，即为以index i为右边界的子数组数量。时间、空间复杂度都为O(N)<br>2. 三指针法：左指针left1、left2，右指针right。其中右指针不断右移，左指针中，left1停在子数组sum>=goal时（连续0的右侧），left2停在sum>goal时（连续0的左侧）。然后就能通过left1和2的索引值差得到以右指针为右边界的子数组数量。时间复杂度O(N)，空间复杂度O(1) |  ||\*|
| [面试题 17.10. 主要元素](https://leetcode-cn.com/problems/find-majority-element-lcci/) | Boyer-Moore 投票算法 | 1. 初始状态，candidate任意值，count=0。<br>2. 遍历输入数组nums中所有元素。当count=0时，使candidate=nums[i]。否则，当candidate!=nums[i]，count-=1，当candidate==nums[i]，count+=1。<br>3. 如果数组中存在主要元素，当遍历结束，candidate即为该主要元素。否则，candidate可能为任意值。因此需要再一次遍历数组，确认该数字是否为主要元素。 | O(N) |O(1)|\*|
| [91. 解码方法](https://leetcode-cn.com/problems/decode-ways/) | dp | string转int：`n, err := strconv.Atoi(string)` | O(N) |O(1)|√|
| [1818. 绝对差值和](https://leetcode-cn.com/problems/minimum-absolute-sum-difference/) | 二分查找 sort | 1. go中的二分查找：`j := nums.Search(v)` nums是已经排序好的数列 | O(NlogN) |O(N)||
| [1653. 使字符串平衡的最少删除次数](https://leetcode-cn.com/problems/minimum-deletions-to-make-string-balanced/) | dp | 1. go中的空语句（类似python中的pass）直接空着就可以`{}`<br>2. string类型也可以使用for循环迭代，中间的元素应该是char？ | O(N) |O(1)|√|
| [1105. 填充书架](https://leetcode-cn.com/problems/filling-bookcase-shelves/) | dp |  | O(N^2) |O(N)|√|
| [1838. 最高频元素的频数](https://leetcode-cn.com/problems/frequency-of-the-most-frequent-element/) | 排序 滑动窗口 | 1. 先调用一个排序<br>2. 然后使用滑动窗口 | O(NlogN) |O(logN)|√|
| [138. 复制带随机指针的链表](https://leetcode-cn.com/problems/copy-list-with-random-pointer/) | 递归 哈希表 | 1. go的全局变量需要在函数的外部声明：`var hashMap map[*Node]*Node`，然后在函数内赋值：`hashMap = map[*Node]*Node {}`<br>2. 创建一个Node类型的对象，然后将对象地址赋给Node类型指针：`flag := &Node {Val:0}`<br>3. 这是一个使用递归的题目，对于母链表中的节点node，检查hash表中对应的newnode有没有被创建，有创建则返回该newnode，没有被创建则创建newnode，然后将该newnode更新到hash表中，然后继续检查node的next node和random node指向的节点。 | O(N) |O(N)|\*|
| [300. 最长递增子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/) | 贪心 二分法 | 1. 目的是找到最小递增幅度<br>2. 建立一个空序列d，遍历目标数组。当目标数组遍历到的nums[i]>d[-1]时，直接将nums[i]插入d的最后。当nums[i]大于d[-1]时，使用二分法将其替换掉d数组中正好大于nums[i]且小于等于nums[i]的某个数。<br>3. 最后得到的空序列长度即为最长递增子序列长度（但是d并不是最长递增子序列，是一个工具数组） | O(NlogN) |O(N)|\*|
| [1713. 得到子序列的最少操作次数](https://leetcode-cn.com/problems/minimum-operations-to-make-a-subsequence/) | 哈希表 最长递增子序列 | 1. 实际上的解法：将arr中的数字转换成其在target中对应的index，寻找该index序列的最长递增子序列<br>2. 如果直接将arr数字转换成index序列，复杂度为O(NM)，超过题目限制。利用题目中arr中数字不重复的特性，加入哈希表Dict，key为arr中数字，value为对应index。然后再遍历target，如果如果target[i]存在于哈希表的键值中，则查找对应value是否加入该递增子序列。 | O(M+NlogN) |O(N+M)|?|



```go
func in(target string, str_array []string) bool {
    sort.Strings(str_array)
    index := sort.SearchStrings(str_array, target)
    if index < len(str_array) && str_array[index] == target {
        return true
    }
    return false
}
```
### OJ考试笔记


| 功能                          | 例子                                                         | 说明                                                         |
| ----------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| string转换int                 | i, err := strconv.Atoi("12")                                 |                                                              |
| 字符格式的数字比大小          | if timeStr[1]<'4' {}                                         |                                                              |
| Golang中的类型写法            | `type FilterSystem struct {`<br>    `    dataCenter map[string] bool`<br>`}`<br>类型方法：<br>`func (fileterSystem *FilterSystem) add(keyword string) int {}` |                                                              |
| 建议使用constructor初始化类型 | `func Constructor() FilterSystem {`<br>      `data := make(map[string]bool, 0)`<br>      `fileSystem := FilterSystem{data}`<br>      `return fileSystem` <br>`}` |                                                              |
| 确认字典中存在某个key         | if _, ok := dictName[keyword]; ok {}                         |                                                              |
| 字符串分隔                    | strArr := strings.Split([stringName], " ")                   |                                                              |
| 判断前缀 后缀                 | strings.HasPrefix(strName, keyword)<br>strings.HasSuffix(strName, keyword) | 输入是长的在前面短的在后面。返回bool值                       |
| 删除字符串前缀                | strings.TrimPrefix(strName, prefix)                          | 返回删除后的结果，如果字符串和prefix相同就返回“”             |
| 字典可以直接删除关键字        | delete(dictName, keyword)                                    |                                                              |
| 去除字符串前后的空格          | strings.Trim(strName, " ")                                   | strings.Trim(str1, str2)去除str1左右两侧包含在str2中的字符   |
| 反向遍历数组                  | `for i:= range arr {`<br>    `i = len(arr)-1-i`<br>    `...`<br>`}` |                                                              |
| const写法                     | `const a, b=3,5`<br>`const (`<br>    `maxA = 1`<br>    `maxB = 2`<br>`}` |                                                              |
| rune转int                     | int(r - '0')                                                 |                                                              |
| 小数精度限制                  | fmt.Printf("%.5f", c2/c1)                                    |                                                              |
| 降序数组排列                  | sort.Sort(sort.Reverse(sort.IntSlice(s)))                    |                                                              |
| 字符串排序                    | sort.Sort(sort.StringSlice(s))                               |                                                              |
| 字符串连接                    | word = word1+word2<br>word = word1 + string(c)               |                                                              |
| 转进制                        | fmt.Sprintf("%b", n)                                         | %b： 二进制<br>%d：十进制<br>%o：八进制<br>%8b：宽度为8<br>%08b：填充前导0<br>%.2f：小数点后宽度为2<br>fmt.Sprintf("%0*s", maxlen, b)：填充0，maxlen宽度 |
| 求余数                        | x % y                                                        |                                                              |
| 查看对象类型                  | `switch m := target.(type) {`<br>    `case string: `<br>        `\\...`<br>    `case int:`<br>        `\\...`<br>`}` | 其中i.(type)只能在switch中使用                               |
| 删除slice中第i个元素          | result = append(slice[:i], slice[i+1:])                      |                                                              |
| byte和rune                    | byte就是uint8，rune就是int32。byte用于强调数据是raw data，rune用来表示unicode的code point |                                                              |
| 使用指定方法排序              | sort.SliceStable([sliceName], [指定方法func])                |                                                              |
| 字符串比较                    | strings.Compare(str1, str2)                                  | str1<str2：输出-1<br>str1=str2：输出0<br>str1>str2：输出1    |
| 字符串衔接                    | strings.Join(list, " ")                                      |                                                              |
| 连接两个数组                  | a = append(a, b...)                                          |                                                              |

### OJ输入处理

```go
input := bufio.NewScanner(os.Stdin)
// 单独读行
input.Scan()
strArr := strings.Split(input.Text(), " ")
fmt.Println(strArr)

// 重复读行
for input.Scan() {
	strArr := strings.Split(input.Text(), " ")
	fmt.Println(strArr)
}
```

### 创建二维数组

```go
grid := make([][]int, n)
	for i := 0; i < n; i++ {
		grid[i] = make([]int, m)
	}
```

### 材料

[Go语言标准库](https://books.studygolang.com/The-Golang-Standard-Library-by-Example/)

### 排序

默认升序

```go
type Interface interface {
        // 获取数据集合元素个数
        Len() int
        // 如果 i 索引的数据小于 j 索引的数据，返回 true，且不会调用下面的 Swap()，即数据升序排序。
        Less(i, j int) bool
        // 交换 i 和 j 索引的两个元素的位置
        Swap(i, j int)
}
```

需要实现三个接口

### 自定义比较器排序

sort.SliceStable方法可以保证排序的相同输入维持与原先顺序相同的排序

```go
func ExampleSliceStable() {
	people := []struct {
		Name string
		Age  int
	}{
		{"Alice", 25},
		{"Elizabeth", 75},
		{"Alice", 75},
		{"Bob", 75},
		{"Alice", 75},
		{"Bob", 25},
		{"Colin", 25},
		{"Elizabeth", 25},
	}
	sort.SliceStable(people, func(i, j int) bool { return people[i].Name < people[j].Name })
	sort.SliceStable(people, func(i, j int) bool { return people[i].Age < people[j].Age })
}
```



### 对string排序

```go
type sortRunes []rune
func (s sortRunes) Less(i, j int) bool {
    return s[i] < s[j]
}
func (s sortRunes) Swap(i, j int) {
    s[i], s[j] = s[j], s[i]
}
func (s sortRunes) Len() int {
    return len(s)
}
func SortString(s string) string {
    r := []rune(s)
    sort.Sort(sortRunes(r))
    return string(r)
}
func main() {
	s := "asdfghjkl"
	fmt.Println(SortString(s)) // adfghjkls
}
```

### 基本类型排序

```go
import sort
 
func main() {
    intList := []int{2, 4, 3, 5, 7, 6, 9, 8, 1, 0}
    float8List := []float64{4.2, 5.9, 12.3, 10.0, 50.4, 99.9, 31.4, 27.81828, 3.14}
    stringList := []string{"a", "c", "b", "d", "f", "i", "z", "x", "w", "y"}
   
    // 升序排序
    sort.Ints(intList)
    sort.Float64s(float8List)
    sort.Strings(stringList) 
 
    // 降序排序
    sort.Sort(sort.Reverse(sort.IntSlice(intList)))
    sort.Sort(sort.Reverse(sort.Float64Slice(float8List)))
    sort.Sort(sort.Reverse(sort.StringSlice(stringList)))
}
```



### 判断一个数字是否是数字或者是字母

```go
unicode.IsDigit(rune) // 判断是否是数字
unicode.IsLetter(rune) // 判断是否是字母
unicode.IsLower(rune) // 判断是否是小写字母
unicode.IsUpper(rune) // 判断是否是大写字母
unicode.IsSpace(rune) // 判断是否是空格
```

### 大数计算

big.Int包

```go
// 大数乘法
func multiply(a, b string) string {
	fmt.Println(a, b)
	aBig, _ := new(big.Int).SetString(a, 10)
	bBig, _:= new(big.Int).SetString(b,10)
	return fmt.Sprintf("%v", aBig.Mul(aBig, bBig))
}

// a和0进行比较
if  a.Cmp(big.NewInt(0))==0 {
	...
}
```

