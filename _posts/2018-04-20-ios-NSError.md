---
layout: post
title: ios - NSError
date: 2018-04-20
Author: gwl
categories: iOS
tags: [mac]
comments: true
toc: true
---


```
NSError *error = [[NSError alloc] initWithDomain:@"testDomain"
                                            code:9998
                                        userInfo:@{NSLocalizedDescriptionKey:@"错误描述",
                                                   NSLocalizedFailureReasonErrorKey:@"错误原因",
                                                   NSLocalizedRecoverySuggestionErrorKey:@"解决建议",
                                                   NSLocalizedRecoveryOptionsErrorKey:@[@"解决建议可选1",@"解决建议可选2"]}];

// Domain 错误域：产生错误的地方（系统提供了一些定义的域）
/*
 FOUNDATION_EXPORT NSString *const NSCocoaErrorDomain;
 FOUNDATION_EXPORT NSString *const NSPOSIXErrorDomain;
 FOUNDATION_EXPORT NSString *const NSOSStatusErrorDomain;
 FOUNDATION_EXPORT NSString *const NSMachErrorDomain;
 */
NSString *domain = error.domain;

// code：错误码
NSInteger code = error.code;

// userInfo：错误信息（系统提供了很多定义的key）
NSDictionary *userInfo = error.userInfo;

NSString *localizedDescription = userInfo[NSLocalizedDescriptionKey];
NSString *localizedFailureReason = userInfo[NSLocalizedFailureReasonErrorKey];
NSString *localizedRecoverySuggestion = userInfo[NSLocalizedRecoverySuggestionErrorKey];
NSArray *localizedRecoveryOptions = userInfo[NSLocalizedRecoveryOptionsErrorKey];
```