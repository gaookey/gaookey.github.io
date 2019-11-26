---
layout: post
title: iOS - 九宫格布局
date: 2016-12-23
Author: gwl
categories: iOS
tags: [九宫格]
comments: true
---

```
CGFloat y = 50;// y轴 起始位置
CGFloat rows = 5;// 行数
CGFloat xSpace = 20;// 纵间距
CGFloat ySpace = 30;// 横间距
CGFloat w = ([UIScreen mainScreen].bounds.size.width - (rows + 1) * xSpace) / rows;// 控件宽
CGFloat h = 30;// 控件高

for (int i = 0; i < 13; i ++) {
    UIView *v = [[UIView alloc] initWithFrame:CGRectMake( xSpace + (i % (int)rows) * (xSpace + w), y + (i / (int)rows) * ( ySpace + h), w, h)];
    v.backgroundColor = [UIColor redColor];
    [self.view addSubview:v];
}
```
