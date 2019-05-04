# Pow(x, n)

## 题目描述

实现 pow(x, n) ，即计算 x 的 n 次幂函数。

```
输入: 2.00000, 10 输出: 1024.00000

输入: 2.10000, 3 输出: 9.26100

输入: 2.00000, -2 输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25
```

* -100.0 < x < 100.0
* n 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。

## 分析

使用折半计算，每次把n缩小一半，这样n最终会缩小到0，任何数的0次方都为1，这时候我们再往回乘，如果此时n是偶数，直接把上次递归得到的值算个平方返回即可，如果是奇数，则还需要乘上个x的值。
还有一点需要引起我们的注意的是n有可能为负数，对于n是负数的情况，我们可以先用其绝对值计算出一个结果再取其倒数即可。我们让i初始化为n，然后看i是否是2的倍数，是的话x乘以自己，否则result乘以x，i每次循环缩小一半，直到为0停止循环。最后看n的正负，如果为负，返回其倒数。

## 算法

```java
class Solution {
    public double myPow(double x, int n) {
        double result = 1.0;
        for(int i = Math.abs(n); i != 0; i = i >> 1){
            if((i & 1) == 1){
                result *= x;
            }
            x *= x;
        }
        return n>=0 ? result : 1 / result;
    }
}
```