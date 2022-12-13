# 组合总和II

![](Pasted%20image%2020221208223549.png)

## 回溯

相对于[组合总和III](./组合总和III.md)而言此题存在重复元素，需要去重

去重逻辑：使用序列标记使用的元素，在取元素时不取重复元素

数组`used = [0, 0, 0]` 标记，`0`代表未使用，`1`代表使用

- 1、树层去重（for）
- 2、树枝去重（递归）

**去重需要先进行排序**，排序是为了将相同的元素放在一起，当第一个元素作为起始往下搜时，此分支包含后面所有相同元素分支，此时可以去掉后面相同元素的分支。也就是在数层上同一个元素只取一次，但是树枝上是可以取相同但位置不同的元素

```python
class Solution:
	def combinationSum2(self, nums: List[int], target: int) -> List[List[int]]:
		nums.sort()
		res = []
		used = [0 for _ in range(len(nums))]
		def dfs(index, _sum, li, used):
			if _sum > target:
				return           
			if target == _sum:
				res.append(li[:])
	
			for i in range(index, len(nums)):
				if i > 0 and nums[i] == nums[i-1] and used[i-1] == 0:
					continue
	
				# print(i)
				used[i] = 1
				li.append(nums[i])
				_sum += nums[i]
				dfs(i + 1, _sum, li, used)
				li.pop()
				_sum -= nums[i]
				used[i] = 0
	
		dfs(0, 0, [], used)
	
		return res
```


去重部分：需要满足此元素与前一个元素相等，并且前一个元素没有取，如果前一个元素使用了，那么此时是前一个元素下的一个分支，并不是以当前元素开头，所以需要排除此情况

```python
if i > 0 and nums[i] == nums[i-1] and used[i-1] == 0:
	continue
```

其中`used[i-1] == 0`是标记是数层去重

上述是通过used数组来记录是否使用，但是其实`index`就是代表从哪一个元素开头，所以上述的去重部分可以简化为

```python
if i > index and nums[i] == nums[i - 1]:
	continue
```