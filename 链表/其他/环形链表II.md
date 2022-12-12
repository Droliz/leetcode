# 环形链表II

![[Pasted image 20221212191852.png]]

## 题解

### 双指针

判断环形链表很简单，快慢指针即可，但是问题在于如何找到环形的头节点

对于环形的链表有如下情况

![[Pasted image 20221212202238.png]]

需要求$x$的大小，对于快慢指针的走的次数有如下等式慢指针$slowNum = x+y+k(y+z)$ 快指针$fastNum = x+y+n(y+z)$    n一定是比k要大的，否则不可能追上

因为快指针一次走两步，慢指针一次走一步，所以$2(x+y+k(y+z))=x+y+n(y+z)$化简$x=(n-k)(y+z)-y$因为$n-k\geqslant 1$可以化简为$x=(m-1)(y+z)+z$ 其中$m=n-k$所以这里可以很明显如果圈数为一圈那么$$x=z$$
**所以其实论转了多少圈，最后一定会在入口处相遇**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
  
class Solution:
	def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
	
		slow, fast = head, head
	
		while fast and fast.next:
			slow = slow.next
			fast = fast.next.next
			if fast is slow:
				cur = head
				while cur != fast:
					cur = cur.next
					fast = fast.next
				return cur
	
		return None
```


### 哈希表

每一个节点都是唯一的，对于非环形一定不会出现重复的，但是对于环形，第一次出现的重复节点就是环形的入口

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
  
class Solution:
	def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
	
		dic = {}
	
		while head:
			if dic.get(head) is None:
				dic[head] = 1
			else:
				return head
			head = head.next
		return None
```