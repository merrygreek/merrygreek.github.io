---
layout:     post
title:      "python.cookbook-1.20"
subtitle:   "归纳笔记"
date:       2016-11-01
author:     "Deng"
header-img: "img/post-bg-python-1.jpg"
tags:
    - python
---
## 1.6 ##

defaultdict类，直接上代码。

```

from collections import defaultdict

d = defaultdict(list)
d['a'].append(1)
d['a'].append(2)
d['b'].append(3)

d = defaultdict(set)
d['a'].add(0)
d['a'].add(2)

```

创建如下代码
`{'a' : [1, 2], 'b' : [3]}, {'a' : (0, 2)}`

构建一个一键多值的字典：
```

d = {}
for key, value in pairs:
  if key not in d:
    d[key] = []
  d[key].append(value)

```
以上代码显得比较杂乱，不够清晰。
使用defaultdict构建：
```

d = defaultdic(list)
for key, value in pairs:
  d[key].append(value)

```

## 1.7 ##

**让字典保持有序**使用OrderDict类。当对字典进行迭代时，它会严格按照元素初始添加的顺序进行。
```

from collections import OrderDict

d = OrderDict()
d['foo'] = 1
d['bar'] = 2

```
这对构建序列化编码非常有用，例如json数据。
OrderDict 内部维护了一个双向链表，所以**OrderDict大小是普通字典的两倍多**
 

**1.8**

字典相关运算：
prices是一个字典，键是商品，值是价格。利用zip函数将字典键值反转。
    min_prices = min(zip(prices.values(), prices.keys()))

对字典进行排序，只需加上sorted().
    prices_sorted = sorted(zip(prices.values(), prices.keys()))

**zip()创建的是迭代器，内容只能被消费一次**，举例上面min_prices只能被消费一次。


在字典执行数据操作时，他们处理的是键，而不是值。例min(), max(),往往我们需要操作的是值。
```

min(prices)
min(prices.values)
min(prices, key = lambda k: prices[k])

```

## 1.9 ##

字典的一些集合操作：
```

a.keys() & b.keys()
a.keys() - b.keys()
a.items() & b.items()
c = {key:a[key] for key in a.keys() - ['z', 'w']}

```
字典的keys，items支持集合操作，而values不支持。因为字典的值并不能保证唯一，部分原因。

## 2.0 ##

去除序列中重复元素，但仍保持元素顺序不变：
如果序列是可哈希的。
```

def dedupe(items):
  seen = set()
  for item in items:
    if item not in seen:
      yield item
      seen.add(item)

```
使用这个函数，a是一个list，`list(dedupe(a))`
```

def dedupe(items, key=None)
  seen = set()
  for item in items:
    val = item if key is None else key(items)
    if val not in seen:
      yield item
      seen.add(val)

```

用set()可去除重复元素但不能保证元素顺序。
```

with open(file.txt) as f:
  for line in deque(f):

```
去除重复文本行。