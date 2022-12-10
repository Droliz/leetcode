# x的平方根

![[Pasted image 20221210200638.png]]

## 题解

利用二分法查找

```python
class Solution:
    def mySqrt(self, x: int) -> int:
  
        i, j = 0, x
  
        while i <= j:
            mid = i + j >> 1
            if mid * mid == x:
                return mid
            elif mid * mid > x:
                j = mid - 1
            else:
                i = mid + 1
        # print(i, j)
        return i - 1   # 由于向下取整所以 - 1
```