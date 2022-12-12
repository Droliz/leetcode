# 组合总和III

![[Pasted image 20221207174417.png]]

## 回溯


- 1、回溯参数
- 2、终止条件
	- 长度到达就终止，至于是否添加，需要看sum
- 3、单次递归

```python
class Solution:
	def combinationSum3(self, k: int, n: int) -> List[List[int]]:
	
		res = []  # 记录结果
		temp = []  # 记录每一次
	
		def back(k, n, startIndex):
			if len(temp) == k:
				if sum(temp) == n:
					res.append(temp[:])
				return 
			for i in range(startIndex, 9 - (k - len(temp)) + 1):
				temp.append(i + 1)
				back(k, n, i + 1)
				temp.pop()
	
		back(k, n, 0)
	
		return res
```