---
layout: post
title: Java WeakReference 使用错误一例
date: 2017-10-27 15:32:24.000000000 +09:00
tag: Android
---

Java Random 无限循环
--------------------------------------

Code Snippet
```java
        while(node.totalSize <= 0) {
            node.totalSize = random.nextInt(10);
        }
        while(node.sentSize <= 0) {
            node.sentSize = random.nextInt(node.totalSize);
        }
```

Random.nextInt 要求参数必须大于0。



解决方案：

```java
        while(node.totalSize <= 0) {
            node.totalSize = random.nextInt(10);
        }
        while(node.sentSize <= 0) {
            node.sentSize = random.nextInt(node.totalSize+1);
        }
```

或者：
```java
        while(node.totalSize <= 0) {
            node.totalSize = random.nextInt(10);
        }
        node.sentSize = random.nextInt(node.totalSize);
                
```