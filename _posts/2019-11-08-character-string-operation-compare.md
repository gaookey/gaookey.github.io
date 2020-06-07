---
layout: post
title: NSDecimalNumber - 字符串运算/字符串比较数字大小
date: 2019-11-08
Author: gwl
categories: 
tags: []
comments: true
---


```
#import "DecimalNumberHandler.h"

@implementation DecimalNumberHandler

/// 字符串运算/字符串比较数字大小
/// @param frontStr frontStr
/// @param afterStr afterStr
/// @param scale 保留小数点后几位
/// @param type 运算符号 + - * /
/// @param result result:运算结果  compareResult:比较结果(0:frontStr < afterStr 1:frontStr = afterStr 2:frontStr > afterStr)
+ (void)decimalNumberFrontStr:(NSString *)frontStr afterStr:(NSString *)afterStr scale:(short)scale type:(DecimalNumberType)type result:(void (^)(NSString *result,int compareResult))result
{
    NSDecimalNumberHandler *behavior = [NSDecimalNumberHandler
                                        decimalNumberHandlerWithRoundingMode:NSRoundUp
                                        scale:scale
                                        raiseOnExactness:NO
                                        raiseOnOverflow:NO
                                        raiseOnUnderflow:NO
                                        raiseOnDivideByZero:YES];
    
    NSDecimalNumber *frontNum = [NSDecimalNumber decimalNumberWithString:frontStr];
    NSDecimalNumber *afterNum = [NSDecimalNumber decimalNumberWithString:afterStr];
    
    NSDecimalNumber *resultNum = [[NSDecimalNumber alloc] init];
    
    switch (type) {
        case DecimalNumberTypeAdding:
            resultNum = [frontNum decimalNumberByAdding:afterNum
                                           withBehavior:behavior];
            break;
        case DecimalNumberTypeSubtracting:
            resultNum = [frontNum decimalNumberBySubtracting:afterNum
                                                withBehavior:behavior];
            break;
        case DecimalNumberTypeMultiplying:
            resultNum = [frontNum decimalNumberByMultiplyingBy:afterNum
                                                  withBehavior:behavior];
            break;
        case DecimalNumberTypeDividing:
            resultNum = [frontNum decimalNumberByDividingBy:afterNum
                                               withBehavior:behavior];
            break;
            
        default:
            break;
    }
    
    NSArray *arr = [[NSString stringWithFormat:@"%@",resultNum] componentsSeparatedByString:@"-"];
    NSString *str = arr.count == 1 ? arr[0] : arr[1];
    
    // 比较两个值的大小
    NSDecimalNumber *front = [NSDecimalNumber decimalNumberWithString:frontStr];
    NSDecimalNumber *after = [NSDecimalNumber decimalNumberWithString:afterStr];
    
    NSComparisonResult compare = [front compare:after];
    int compareResult = 0;
    
    if (compare == NSOrderedAscending) {// 升序
        compareResult = 0;
    } else if (compare == NSOrderedSame) {// 相等
        compareResult = 1;
    } else if (compare == NSOrderedDescending) {// 降序
        compareResult = 2;
    }
    
    result(str,compareResult);
}

@end
```
