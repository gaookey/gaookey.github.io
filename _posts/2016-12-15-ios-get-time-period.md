---
layout: post
title: iOS 获取时间段
date: 2016-12-15
Author: gwl
categories: iOS
tags: [NSCalendar, NSDateComponents, NSDate]
comments: false
toc: true
---





```objectivec
/// 18:00:00 -> 18   /   18:00:01 -> 19
- (NSInteger)getTimePeriod:(NSDate *)date {
    for (NSInteger i = 1; i <= 24; i ++) {
        if ([date compare:[self getCustomDateWithHour:i - 1 date:date]] == NSOrderedDescending && [date compare:[self getCustomDateWithHour:i date:date]] == NSOrderedAscending) {
            return i;
        }
        if ([date compare:[self getCustomDateWithHour:i date:date]] == NSOrderedSame) {
            return i;
        }
    }
    return 0;
}
- (NSDate *)getCustomDateWithHour:(NSInteger)hour date:(NSDate *)date {
    NSCalendar *currentCalendar = [[NSCalendar alloc] initWithCalendarIdentifier:NSCalendarIdentifierGregorian];
    NSDateComponents *currentComps = [[NSDateComponents alloc] init];
    NSInteger unitFlags = NSCalendarUnitYear | NSCalendarUnitMonth | NSCalendarUnitDay | NSCalendarUnitHour | NSCalendarUnitMinute | NSCalendarUnitSecond;
    
    currentComps = [currentCalendar components:unitFlags fromDate:date];
    
    NSDateComponents *resultComps = [[NSDateComponents alloc] init];
    [resultComps setYear:[currentComps year]];
    [resultComps setMonth:[currentComps month]];
    [resultComps setDay:[currentComps day]];
    [resultComps setHour:hour];

    NSCalendar *resultCalendar = [[NSCalendar alloc] initWithCalendarIdentifier:NSCalendarIdentifierGregorian];
    return [resultCalendar dateFromComponents:resultComps];
}
```
