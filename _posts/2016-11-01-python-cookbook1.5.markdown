---
layout:     post
title:      "python.cookbook-1.5"
subtitle:   "归纳笔记"
date:       2016-11-01
author:     "Deng"
header-img: "img/post-bg-python.jpg"
tags:
    - python
---



## 1.1 ##

分解操作，丢弃某些特定的值。

```

data = ['huawei', 20, 1222, (2014, 12, 3)]

_, share, price, _ = data

```

		
## 1.2 ##

可迭代对象分解出元素，***表达式**取其中元素。

    first *middle, last = grades

*表达式语法迭代一个变长元组，特别有用。

    for tag, *args in records:

函数参数：`foo(*args)`

与字符串处理相结合：
    `uname, *fields, homedir, sh = line.split(':')`

特定位置丢弃：`name, *_, (*_, year) = record`

实现的递归语法：
    
```
def sum(items):

	 head, *tail = items

	 return head + sum(tail) if tail else head
```


## 1.3 ##

保留最后的N个元素

    deque(maxlen=N)`创建了一个固定长度的队列，方法有append（）

需要一个简单的队列结构时，用deque。**不指定队列大小，得到一个无界限的队列**

deque队列可以从两边插入，append()，appendleft() 也可以从两边弹出，pop()，popleft()  **复杂度O(1)**,列表**O(N)**
 

**保存有限记录，collections.deque 完美应用场景**

```
from collections import deque

def search(lines, pattern, history=5):
  previous_lines = deque(maxlen=history)
  for line in lines:
    if pattern in line:
		yield line, previous_lines
	previous_lines.append(line)

if __name__ = '__main__':
	with open('file.txt') as f:
		for line, prevlines in search(f, 'python', 4):
			for pline in prevlines:
				print(pline, end='')
			print(line, end='')
			print('-'*20)

```
  
## 1.4 ##

集合中找出最大or最小的N个元素

    heapq.nlargest(2, nums), heapq.nsmallest(2, nums)

函数可以接受key参数，应用更复杂的数据结构。

    heapq.nlargest(3, info, key=lambda s: s[price])

## 1.5 ##

实现优先级队列

看heapq文档