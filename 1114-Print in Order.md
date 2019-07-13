# Print in Order

## 题目描述

Suppose we have a class:

```java
public class Foo {
  public void one() { print("one"); }
  public void two() { print("two"); }
  public void three() { print("three"); }
}
```

The same instance of Foo will be passed to three different threads. Thread A will call one(), thread B will call two(), and thread C will call three(). Design a mechanism and modify the program to ensure that two() is executed after one(), and three() is executed after two().

```
Input: [1,2,3]
Output: "onetwothree"
Explanation: There are three threads being fired asynchronously. The input [1,2,3] means thread A calls one(), thread B calls two(), and thread C calls three(). "onetwothree" is the correct output.

Input: [1,3,2]
Output: "onetwothree"
Explanation: The input [1,3,2] means thread A calls one(), thread B calls three(), and thread C calls two(). "onetwothree" is the correct output.

```

Note: We do not know how the threads will be scheduled in the operating system, even though the numbers in the input seems to imply the ordering. The input format you see is mainly to ensure our tests' comprehensiveness.

## 分析

使用 `java.util.concurrent` 并发包中的 `Lock` 进行加锁，使用 `Condition` 控制方法执行顺序。

## 算法

```java
class Foo {

    private java.util.concurrent.locks.Lock lock;
    private java.util.concurrent.locks.Condition c1;
    private java.util.concurrent.locks.Condition c2;
    
    public Foo() {
        lock = new java.util.concurrent.locks.ReentrantLock();
        c1 = lock.newCondition();
        c2 = lock.newCondition();
    }

    public void first(Runnable printFirst) throws InterruptedException {
        
        // printFirst.run() outputs "first". Do not change or remove this line.
        try{
            lock.lock();
            printFirst.run();
            c1.signal();
        }finally{
            lock.unlock();
        }
    }

    public void second(Runnable printSecond) throws InterruptedException {
        
        // printSecond.run() outputs "second". Do not change or remove this line.
        try{
            lock.lock();
            c1.await();
            printSecond.run();
            c2.signal();            
        }finally{
            lock.unlock();
        }
    }

    public void third(Runnable printThird) throws InterruptedException {
        
        // printThird.run() outputs "third". Do not change or remove this line.
        try{
            lock.lock();
            c2.await();
            printThird.run();
        }finally{
            lock.unlock();   
        }
    }
}
```