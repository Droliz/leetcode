# 全排列II

![[Pasted image 20221209133110.png]]

## 回溯

相对于[全排列](./全排列.md)而言，全排列II存在重复元素，所有需要进行剪枝（去重）

假设数组`[1, 1, 2]`计算，那么有如下树形结构

![[Pasted image 20221209135052.png]]


通过树形结构，可以很轻松知道前面使用过的元素，后面再使用就会重复

所以是树层上去重，树枝上可以取

```python
class Solution:
	def permuteUnique(self, nums: List[int]) -> List[List[int]]:
	
		nums.sort()
		res = []
		path = []
		used = [0 for _ in range(len(nums))]
		def back():
			if len(path) == len(nums):
				res.append(path[:])
				return
	
			for i in range(len(nums)):
				if i > 0 and nums[i] == nums[i-1] and used[i-1] == 0: continue
				if used[i] == 1: continue
				used[i] = 1
				path.append(nums[i])
				back()
				path.pop()
				used[i] = 0
		back()
	
		return res
``` 

注意这里去重的逻辑中，是`continue`不是`break`，如果是`return`或`break`会导致后面的数没有取到

