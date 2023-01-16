# KMP算法

## 介绍

KMP算法是用于解决字符串匹配问题

字符串`aabaabaaf`模式串`aabaaf`（子串），在字符串中是否出现过模式串

## 匹配字符串解法

### 暴力解法

两层`for`循环，将每个字符作为开头，直到匹配上 $O(mn)$

### KMP算法

$O(n)$

对于暴力解法，每次不匹配都跳回到最开始，然后对下一个字符开始重新匹配。那么KMP就是在这个过程中发现字符不匹配，由于已经遍历过字符（利用这些信息来避免暴力算法中的回退）。
KMP中使用数组`next`来实现，当不匹配时，就会查找最后一个匹配的字符`next`中的数值，然后子串对应跳转到`next`这个位置继续匹配

```python
def kmp_search(string, patt):
	# next数组
	next = build_next(patt)

	# 指针
	i = 0   # 主串中的指针
	j = 0   # 子串中的指针
	while i < len(string):
		# 字符串匹配，指针后移
		if string[i] == patt[j]:
			i += 1
			j += 1
		elif j > 0:   # 未匹配上，更新子串指针位置
			j = next[j-1]
		else:    # j = 0 就匹配失败，向后移
			i += 1
		# 匹配成功
		if j == len(patt):
			return i - j
```

那么`next`代表的就是可以跳过的子串匹配的数量，由于当前的匹配失败，那么在当前之前的一定是匹配成功的也就是说，如果有`aabaabaaf`与`aabaaf`在`5`处匹配失败，那么此时对应已经匹配上的`aabaa`可以看作有`abaa、baa、aa、a`，只需要子串前缀中与后缀中这几个最长相等，就代表可以不用重复匹配几个。前缀`a、aa、aab、aaba`，最长相等为`aa`，所以此时可以跳到`aa`后面，也就是最长相等前后缀的长度

`next`数组求解

```python
def bulid_next(patt):
	next = [0]   
	prefix_len = 0  # 计算相等前后缀长度（相当于前缀末尾）
	i = 1   # 后缀末尾
	while i < len(patt):
		
		if patt[prefix_len] == patt[i]:
			prefix_len += 1
			next.append(prefix_len)
			i += 1
		else:
			if prefix_len == 0:
				next.append(0)
				i += 1
			else:
				prefix_len = next[prefix_len - 1]
	return next
```

在求最长相等前后缀时，需要两个指针，一个指向前缀末尾，一个指向后缀末尾。而`next`数组的值其实就是前缀末尾

[KMP算法讲解](https://www.bilibili.com/video/BV1AY4y157yL/?spm_id_from=333.337.search-card.all.click&vd_source=1ad6474edf4c8b8b8ad080b520386b0c)


### 前缀表

在一个字符串中，前缀代表由`0索引`开头，不包含结尾的所有子串。后缀代表不包含`0索引`，到达结尾的所有子串。前缀表代表这个字符串的前缀和后缀相等的**最大长度**

当匹配`aabaaf`与`aabaabaaf`时，匹配到`b`会发现`b与f`不匹配。此时在已经匹配的`aabaa`中，可以发现最大后缀`aa`与最大前缀`aa`，那么此时可以跳到`b`位置。因为后面`aa`已经是源字符串匹配上的，就相当于找到前缀开始重新匹配