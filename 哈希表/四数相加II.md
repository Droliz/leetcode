# 四数相加II

![](Pasted%20image%2020221214115831.png)

## 题解

此题在四个数组中，所以不用考虑到去重。

假设每个数组取出的值为`a、b、c、d`那么就有 $a+b+c+d=0$ 所以很容易想到暴力解法四个循环，同时可以化简为`a、b、c`然后判断`d`的存在性，既然如此那么其实还可以化简为 $(a+b)+(c+d)=0$ 此时就想两数之和一样，那么很容易就想到`map`解决

```python
class Solution:
	def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
	
		dic = dict()
		res = 0
		# 初始化
		for a in nums1:
			for b in nums2:
				if a + b in dic:
					dic[a+b] += 1
				else:
					dic[a+b] = 1
		# 判断
		for c in nums3:
			for d in nums4:
				temp = -c-d
				if temp in dic:
					res += dic[temp]
	
		return res
```


