---
layout: post
title: iOS NSDecimalNumber
date: 2019-11-08
Author: gwl
categories: 
tags: []
comments: false
toc: true
---





##### 基本运算

```swift
let num = NSDecimalNumber(string: "35.89302")
let num2 = NSDecimalNumber(string: "15.161")

var result = NSDecimalNumber()

// 加  51.05402
result = num.adding(num2)
// 减  20.73202
result = num.subtracting(num2)
// 乘  544.17407622
result = num.multiplying(by: num2)
// 除  2.36745729173537365609128685442912736626
result = num.dividing(by: num2)
// 次方  1288.3088847204
result = num.raising(toPower: 2)
```





---



##### 设置小数点后保留位数 

```swift
/*
 NSDecimalNumber.RoundingMode :
 
 value    1.2  1.21  1.25  1.35  1.27
 
 plain    1.2  1.2   1.3   1.4   1.3
 down     1.2  1.2   1.2   1.3   1.2
 up       1.2  1.3   1.3   1.4   1.3
 bankers  1.2  1.2   1.2   1.4   1.3
 */
 
let behavior = NSDecimalNumberHandler(roundingMode: .bankers,
                                      scale: 2, // 保留两位小数
                                      raiseOnExactness: false,
                                      raiseOnOverflow: false,
                                      raiseOnUnderflow: false,
                                      raiseOnDivideByZero: true)

let num = NSDecimalNumber(string: "35.89302")
let num2 = NSDecimalNumber(string: "15.161")
var result = NSDecimalNumber()

// 除  2.37
result = num.dividing(by: num2, withBehavior: behavior)
```





##### 比较大小



```swift
let num = NSDecimalNumber(string: "35.89302")
let num2 = NSDecimalNumber(string: "15.161")

// num > num2
let result = num.compare(num2)

if result == .orderedAscending {
    print("num < num2")
} else if result == .orderedDescending {
    print("num > num2")
} else if result == .orderedSame {
    print("num == num2")
}
```

