# N皇后

![[Pasted image 20221209161416.png]]

## 回溯

![[Pasted image 20221209162050.png]]

与其他的回溯问题不同的是，N皇后属于二维的，相对于其他的一维的会难很多

棋盘问题递归的深度取决于棋盘的高度，`for`取决于棋盘宽度

```python
class Solution:
	def solveNQueens(self, n: int) -> List[List[str]]:
	
		res = []   # 结果集
		path = [["."] * n for _ in range(n)]  # 每个结果
	
		def back(row):
			if row == n:
				res.append([''.join(tmp) for tmp in path])
				return
			for col in range(n):
				# 判断合法棋盘
				if isValid(row, col, path):
					path[row][col] = 'Q'
					back(row + 1)
					path[row][col] = '.'
	
		 # 判断棋盘合法性
		def isValid(row, col, path):
			# 检查竖直
			for i in range(n):
				if path[i][col] == 'Q':
					return False
			# 检查45%斜角
			x = col + 1
			y = row - 1
			while y >= 0 and x < len(path): 
				if path[y][x] == 'Q':
					return False
				x += 1
				y -= 1
			# 检查135%斜角
			x = col - 1
			y = row - 1
			while y >= 0 and x >= 0: 
				if path[y][x] == 'Q':
					return False
				x -= 1
				y -= 1
	
			return True
	
		back(0)
	
		return res
```