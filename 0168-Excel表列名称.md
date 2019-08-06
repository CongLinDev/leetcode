# Excel表列名称

## 题目描述

给定一个正整数，返回它在 Excel 表中相对应的列名称。

```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB
    ...
```

## 分析

将整数转为26进制（`n--`即将 `0-25` 对应于 `A-Z`）。

## 算法

```java
class Solution {
    public String convertToTitle(int n) {
        StringBuilder s = new StringBuilder();

        while(n-- != 0){
            s.append((char)(n % 26 + 'A'));
            n /= 26;
        }
        return s.reverse().toString();
    }
}
```
