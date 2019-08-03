# Excel表列序号

## 题目描述

给定一个Excel表格中的列名称，返回其相应的列序号。

```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28
    ...
```

## 分析

## 算法

```java
class Solution {
    public int titleToNumber(String s) {
        int count = 0;
        for(char ch : s.toCharArray()){
            count *= 26;
            count += (ch - 'A' + 1);
        }
        return count;
    }
}
```
