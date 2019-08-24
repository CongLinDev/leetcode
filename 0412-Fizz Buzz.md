# Fizz Buzz

## 题目描述

写一个程序，输出从 1 到 n 数字的字符串表示。

1. 如果 n 是3的倍数，输出“Fizz”；
2. 如果 n 是5的倍数，输出“Buzz”；
3.如果 n 同时是3和5的倍数，输出 “FizzBuzz”。

```
n = 15,

返回:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```

## 分析

正常比较即可。

## 算法

```java
class Solution {
    public List<String> fizzBuzz(int n) {
        List<String> list = new ArrayList<>(n << 1);
        for(int i = 1; i <= n; i++){
            boolean three = i % 3 == 0;
            boolean five = i % 5 == 0;
            if(three && five){
                list.add("FizzBuzz");
            }else if(three){
                list.add("Fizz");
            }else if(five){
                list.add("Buzz");
            }else{
                list.add(String.valueOf(i));
            }
        }
        return list;
    }
}
```
