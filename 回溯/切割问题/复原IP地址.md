# 复原IP地址

![](Pasted%20image%2020221208174712.png)

## 回溯

类似回文串分割，不过在剪枝时注意条件不要漏掉

```python
class Solution:  
    def restoreIpAddresses(self, s: str) -> List[str]:  
  
        res = []  
        path = []  
  
        def back(index):  
            # 终止条件  
            if index == len(s):  
                if len(path) == 4:  
                    res.append(".".join(path[:]))  
                return  
  
            # 单层递归操作  
            for i in range(index, len(s)):  
                # 切割串  
                s_1 = s[index: i + 1]  
                # print(s_1)  
                # 剪枝（长度不大于3、没有前导0、符合范围）  
                if len(s_1) > 3 \  
                        or (len(s_1) != 1 and s_1[0] == "0") \  
                        or int(s_1) > 255:     
                    return                   
				path.append(s_1)  
                back(i+1)  
                path.pop()  
  
        back(0)  
  
        return res
```

