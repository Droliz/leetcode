# 删除链表的倒数第n个节点




## 题解

很容易想到直接获取链表长度，然后遍历找到位置删除即可

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
	def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
	
		l = 0
		cur = head
		while cur:
			cur = cur.next
			l += 1
		if l == n:
			return head.next
		cur = head
		# print(cur.val)
		i = l - n + 1
		# print(i)
		for _ in range(i - 2):
			cur = cur.next
		# print(cur.val)
		cur.next = cur.next.next        
		return head
```