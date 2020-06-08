---
layout: post
title: iOS 判断设备型号
date: 2019-10-18
Author: gwl
categories: 
tags: []
comments: false
toc: true
---


### 判断型号

> https://www.theiphonewiki.com/wiki/Models#cite_note-china-1

导入头文件

```objective-c
#include <sys/sysctl.h>
```

![img](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```objective-c
- (NSString *)modelsString {
    size_t size;
    int nR = sysctlbyname("hw.machine", NULL, &size, NULL, 0);
    char *machine = (char *)malloc(size);
    nR = sysctlbyname("hw.machine", machine, &size, NULL, 0);
    NSString *platform = [NSString stringWithCString:machine encoding:NSUTF8StringEncoding];
    free(machine);
    
    return platform;
}
```

![img](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### SPDeviceModels

iOS 设备型号判断

使用 `CocoaPods` 安装: `pod 'SPDeviceModels'`

部分代码如下，最新代码移步 [github](https://github.com/mouos/GWLDeviceModels)

```objective-c
#import <Foundation/Foundation.h>

NS_ASSUME_NONNULL_BEGIN

typedef NS_ENUM(NSInteger, DeviceModelsType) {
    DeviceModelsTypeUnknown,
    
    DeviceModelsTypeSimulator,
    
    DeviceModelsTypeIPhone,
    DeviceModelsTypeIPhone3G,

    ......
};

@interface SPDeviceModels : NSObject

+ (void)modelsString:(void (^)(NSString *string))modelsString modelsType:(void (^)(DeviceModelsType type))modelsType ;

@end

NS_ASSUME_NONNULL_END
```

![img](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```objective-c
#import "SPDeviceModels.h"
#include <sys/sysctl.h>

@implementation SPDeviceModels

+ (void)modelsString:(void (^)(NSString * _Nonnull))modelsString modelsType:(void (^)(DeviceModelsType))modelsType {
    DeviceModelsType type = DeviceModelsTypeUnknown;
    NSString *string = @"Unknown";
    
    size_t size;
    int nR = sysctlbyname("hw.machine", NULL, &size, NULL, 0);
    char *machine = (char *)malloc(size);
    nR = sysctlbyname("hw.machine", machine, &size, NULL, 0);
    NSString *platform = [NSString stringWithCString:machine encoding:NSUTF8StringEncoding];
    free(machine);
    
    
#pragma mark - iPad
    if ([platform isEqualToString:@"iPad1,1"]) {
        type = DeviceModelsTypeIPad;
        string = @"iPad (A1219/A1337)";
    }

    ......
}

@end
```


> 最后更新日期 2020-06-06