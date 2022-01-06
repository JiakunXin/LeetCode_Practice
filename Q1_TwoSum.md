# 两数之和

[题目链接](https://leetcode-cn.com/problems/two-sum/)

**思路**：字典采用Hashmap的形式对key进行储存，因此查询字典是否包含某个key的时间复杂度是O(1)的，但是使用了字典对历史数据进行存储，相当于以空间换时间。

```python
def two_sum(nums: List[int], target: int) -> List[int]:
    
    num_dict = {}

    for i in range(len(nums)):
        num = nums[i]
        if target-num in num_dict:
            return [num_dict[target-num], i]
        else:
            num_dict[num] = i 
```
