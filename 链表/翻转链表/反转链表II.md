## 反转链表II

![[Pasted image 20221211215055.png]]

## 题解

`[1, 2, 3, 4, left, xxxx, right, xxxx]`

反转一部分链表需要获得三部分

- 1、`[head, XXXX, left - 1]`
- 2、`[left, XXXX, right]`
- 3、`[right + 1, XXXX, None]`

那么就需要先获取左边界前一个节点`left-1`处，然后从`left`处遍历`right-left+1`得到`right`的位置，此时已经获取到了需要反转的以及左边的，最后右边的只需要中间的`next`就可以了

最后对中间的链表进行反转，拼接。因为反转之后的链表原先的头节点会变成尾节点，所以可以直接进行拼接


```python
class Solution:
	def reverseBetween(self, head: ListNode, left: int, right: int) -> ListNode:
		# 翻转链表
		def rev(head):
			pre = None
			head_h = head
			while head_h:
				next = head_h.next
				head_h.next = pre
				pre, head_h = head_h, next
			return pre
		res = cur = ListNode(-1)
		cur.next = head
		# 找到左节点的前一个节点
		for _ in range(left - 1):
			cur = cur.next
		# left_h指向左节点的前节点        
		left_h = cur 
		# left_n才是需要翻转的链表的头节点
		left_n = cur.next
		# 找到右节点
		for _ in range(right - left + 1):
			cur = cur.next
		# 记录被断开链表的头节点
		right_h = cur.next
		# 使left_n的尾节点指向None
		cur.next = None
	
		# 将left_h拼接翻转的链表
		left_h.next = rev(left_n)
		# 拼接上right_h
		left_n.next = right_h
	
		return res.next
```