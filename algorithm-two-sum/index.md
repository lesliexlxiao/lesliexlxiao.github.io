# 两数之和


## 1. 题目描述
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那两个整数，并返回他们的数组下标。
你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

## 2. 示例

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9

所以返回 [0, 1]


## 3. 解法

### 3.1 暴力解法
```go
func TwoSum(nums []int, target int) []int {
    var ret []int

    for index1, num1 := range nums {
        for index2, num2 := range nums {
            if index1 != index2 && num1 + num2 == target {
                ret = []int{index1, index2}
                break
            }
        }
        if ret != nil {
            break
        }
    }
    return ret
}
```

- 时间复杂度：O(n^2)

- 空间复杂度：O(1)

### 3.2 一遍哈希表
```go
func TwoSum(nums []int, target int) []int {
    var ret []int
    numsMap := make(map[int]int)

    for index, num := range nums {
        subductionNum := target - num
        if _, ok := numsMap[subductionNum]; ok {
            ret = []int{numsMap[subductionNum], index}
        } else {
            numsMap[num] = index
        }
    }

    return ret
}
```

- 时间复杂度：O(n)

- 空间复杂度：O(n)

## 4. 来源
LeetCode：https://leetcode-cn.com/problems/two-sum

## 5. 参考文章
[1] https://blazehu.github.io/2020/05/12/1.%20%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C/#more
