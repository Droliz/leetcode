# 反转字符串||

![](Pasted%20image%2020221217124021.png)

## 题解

```python
class Solution:
	def reverseStr(self, s: str, k: int) -> str:
		if len(s) < 2:
			return s
		li = list(s)
	
		for i in range(0, len(li), 2 * k):
			li[i: i + k] = self.reverse(li[i: i + k])
		return "".join(li)
	
	def reverse(self, txt):
		i, j = 0, len(txt) - 1
		while i < j:
			txt[i], txt[j] = txt[j], txt[i]
			i += 1
			j -= 1
		return txt
```