# 螺旋矩阵II
![](Pasted%20image%2020221211050130.png)


## 题解

**模拟**

同[螺旋矩阵](./螺旋矩阵.md)

```python
class Solution:
	def generateMatrix(self, n: int) -> List[List[int]]:
	
		res = [[0 for _ in range(n)] for _ in range(n)]
	
		up, down = 0, n - 1
		left, right = 0, n - 1
		num = 1
		while up <= down and left <= right:
			for i in range(left, right + 1):
				res[up][i] = num
				num += 1
			up += 1
			for i in range(up, down + 1):
				res[i][right] = num
				num += 1
			right -= 1
			if up > down: break
			for i in range(right, left - 1, -1):
				res[down][i] = num
				num += 1
			down -= 1
			if left > right: break
			for i in range(down, up - 1, -1):
				res[i][left] = num
				num += 1
			left += 1
		return res
```