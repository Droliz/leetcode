# 子集I

![](Pasted%20image%2020221208192759.png)

## 回溯

子集问题需要注意，同样的没有顺序区别，所以采用index控制，避免重复，类似组合

```python
class Solution:
	def subsets(self, nums: List[int]) -> List[List[int]]:
	
		res = []
		path = []
	
		def back(nums, index):
			res.append(path[:])  # 每次都有收获结果
	
			if index >= len(nums):
				return
			for i in range(index, len(nums)):
				path.append(nums[i])
				back(nums, i + 1)
				path.pop()
		back(nums, 0)
	
		return res
```

此情况收获结果需要在终止之前，否则会导致叶子节点处没有取到