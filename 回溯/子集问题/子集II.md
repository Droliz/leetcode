# 子集II

![[Pasted image 20221208195458.png]]

## 回溯

在[子集I](./子集I.md)的基础上，存在重复元素，所以对于计算的子集存在去重操作

```python
class Solution:
	def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
		nums.sort()
		res = []
		path = []
		def back(nums, index):
			res.append(path[:])
			if index >= len(nums):
				return
	
			for i in range(index, len(nums)):
				if i > index and nums[i] == nums[i-1]:
					continue
				path.append(nums[i])
				back(nums, i + 1)
				path.pop()
		back(nums, 0)
	
		return res
```

去重可以参考[组合总和II](../组合类型/组合总和II.md)