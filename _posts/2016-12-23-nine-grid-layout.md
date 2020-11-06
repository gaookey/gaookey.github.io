---
layout: post
title: iOS 九宫格布局
date: 2016-12-23
Author: gwl
categories: iOS
tags: [九宫格]
comments: false
toc: true
---


# OC
```objectivec
CGFloat y = 50;
CGFloat rows = 5;
CGFloat xSpace = 25;
CGFloat ySpace = 25;
CGFloat width = ([UIScreen mainScreen].bounds.size.width - (rows + 1) * xSpace) / rows;
CGFloat height = 100;

for (NSInteger i = 0; i <= 10; i ++) {
    UIView *v = [[UIView alloc] init];
    v.frame = CGRectMake(xSpace + (i % (int)rows) * (xSpace + width), y + (i / (int)rows) * (ySpace + height), width, height);
    v.backgroundColor = [UIColor orangeColor];
    [self.view addSubview:v];
}
```
# swift
```swift
let y: CGFloat = 50
let rows: CGFloat = 5
let xSpace: CGFloat = 25
let ySpace: CGFloat = 25
let width: CGFloat = (UIScreen.main.bounds.size.width - (rows + 1) * xSpace) / rows
let height: CGFloat = 100

for i in 0...10 {
    let v = UIView()
    v.frame = CGRect(x: xSpace + (CGFloat(i).truncatingRemainder(dividingBy: rows)) * (xSpace + width), y: y + CGFloat(i / Int(rows)) * (ySpace + height), width: width, height: height)
    v.backgroundColor = .orange
    view.addSubview(v)
}
```
