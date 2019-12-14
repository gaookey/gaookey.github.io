---
layout: post
title: iOS判断设备型号
date: 2019-10-18
Author: gwl
categories: 
tags: []
comments: true
---



> [https://www.theiphonewiki.com/wiki/Models#cite_note-china-1](https://www.theiphonewiki.com/wiki/Models#cite_note-china-1)


```
#import <Foundation/Foundation.h>

NS_ASSUME_NONNULL_BEGIN

typedef NS_ENUM(NSInteger, DeviceModelsType) {
    DeviceModelsTypeIPhoneNone,
    
    DeviceModelsTypeIPhoneSimulator,
    
    DeviceModelsTypeIPhone,
    DeviceModelsTypeIPhone3G,
    DeviceModelsTypeIPhone3GS,
    DeviceModelsTypeIPhone4,
    DeviceModelsTypeIPhone4S,
    DeviceModelsTypeIPhone5,
    DeviceModelsTypeIPhone5C,
    DeviceModelsTypeIPhone5S,
    DeviceModelsTypeIPhone6,
    DeviceModelsTypeIPhone6Plus,
    DeviceModelsTypeIPhone6S,
    DeviceModelsTypeIPhone6SPlus,
    DeviceModelsTypeIPhoneSE,
    DeviceModelsTypeIPhone7,
    DeviceModelsTypeIPhone7Plus,
    DeviceModelsTypeIPhone8,
    DeviceModelsTypeIPhone8Plus,
    DeviceModelsTypeIPhoneX,
    DeviceModelsTypeIPhoneXR,
    DeviceModelsTypeIPhoneXS,
    DeviceModelsTypeIPhoneXSMax,
    DeviceModelsTypeIPhone11,
    DeviceModelsTypeIPhone11Pro,
    DeviceModelsTypeIPhone11ProMax,
    
    DeviceModelsTypeIPodTouch,
    DeviceModelsTypeIPodTouch2,
    DeviceModelsTypeIPodTouch3,
    DeviceModelsTypeIPodTouch4,
    DeviceModelsTypeIPodTouch5,
    DeviceModelsTypeIPodTouch6,
    DeviceModelsTypeIPodTouch7,
    
    DeviceModelsTypeIPadMini,
    DeviceModelsTypeIPadMini2,
    DeviceModelsTypeIPadMini3,
    DeviceModelsTypeIPadMini4,
    DeviceModelsTypeIPadMini5,
    
    DeviceModelsTypeIPad,
    DeviceModelsTypeIPad2,
    DeviceModelsTypeIPad3,
    DeviceModelsTypeIPad4,
    DeviceModelsTypeIPad5,
    DeviceModelsTypeIPad6,
    
    DeviceModelsTypeIPadPro12_9,
    DeviceModelsTypeIPadPro2_12_9,
    DeviceModelsTypeIPadPro3_12_9,
    DeviceModelsTypeIPadPro9_7,
    DeviceModelsTypeIPadPro10_5,
    DeviceModelsTypeIPadPro11,
    
    DeviceModelsTypeIPadAir,
    DeviceModelsTypeIPadAir2,
    DeviceModelsTypeIPadAir3
};

@interface DeviceModels : NSObject

+ (instancetype)sharedInstance ;

- (DeviceModelsType)modelsType ;

- (NSString *)modelsString ;

@end

NS_ASSUME_NONNULL_END
```


```
#import "DeviceModels.h"
#include <sys/sysctl.h>

@interface DeviceModels()

@property (assign, nonatomic) DeviceModelsType deviceModelsType;

@end

@implementation DeviceModels

static DeviceModels *instance = nil;

+ (instancetype)sharedInstance {
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        instance = [[[self class] alloc] init];
    });
    return instance;
}

+ (instancetype)allocWithZone:(struct _NSZone *)zone {
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        instance = [super allocWithZone:zone];
    });
    return instance;
}

- (id)copyWithZone:(struct _NSZone *)zone {
    return instance;
}

- (DeviceModelsType)modelsType {
    [self modelsString];
    return instance.deviceModelsType;
}

- (NSString *)modelsString {
    
    size_t size;
    int nR = sysctlbyname("hw.machine", NULL, &size, NULL, 0);
    char *machine = (char *)malloc(size);
    nR = sysctlbyname("hw.machine", machine, &size, NULL, 0);
    NSString *platform = [NSString stringWithCString:machine encoding:NSUTF8StringEncoding];
    free(machine);
    
#pragma mark - iPhone
    if ([platform isEqualToString:@"iPhone1,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone;
        return @"iPhone (A1203)";
    }
    if ([platform isEqualToString:@"iPhone1,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone3G;
        return @"iPhone 3G (A1241/A1324)";
    }
    if ([platform isEqualToString:@"iPhone2,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone3GS;
        return @"iPhone 3GS (A1303/A1325)";
    }
    if ([platform isEqualToString:@"iPhone3,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone4;
        return @"iPhone 4 (A1332)";
    }
    if ([platform isEqualToString:@"iPhone3,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone4;
        return @"iPhone 4 (A1332)";
    }
    if ([platform isEqualToString:@"iPhone3,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone4;
        return @"iPhone 4 (A1349)";
    }
    if ([platform isEqualToString:@"iPhone4,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone4S;
        return @"iPhone 4S (A1387/A1431)";
    }
    if ([platform isEqualToString:@"iPhone5,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone5;
        return @"iPhone 5 (A1428)";
    }
    if ([platform isEqualToString:@"iPhone5,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone5;
        return @"iPhone 5 (A1429/A1442)";
    }
    if ([platform isEqualToString:@"iPhone5,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone5C;
        return @"iPhone 5c (A1456/A1532)";
    }
    if ([platform isEqualToString:@"iPhone5,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone5C;
        return @"iPhone 5c (A1507/A1516/A1526/A1529)";
    }
    if ([platform isEqualToString:@"iPhone6,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone5S;
        return @"iPhone 5s (A1453/A1533)";
    }
    if ([platform isEqualToString:@"iPhone6,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone5S;
        return @"iPhone 5s (A1457/A1518/A1528/A1530)";
    }
    if ([platform isEqualToString:@"iPhone7,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone6;
        return @"iPhone 6 (A1549/A1586/A1589)";
    }
    if ([platform isEqualToString:@"iPhone7,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone6Plus;
        return @"iPhone 6 Plus (A1522/A1524/A1593)";
    }
    if ([platform isEqualToString:@"iPhone8,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone6S;
        return @"iPhone 6s (A1633/A1688/A1691/A1700)";
    }
    if ([platform isEqualToString:@"iPhone8,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone6SPlus;
        return @"iPhone 6s Plus (A1634/A1687/A1690/A1699)";
    }
    if ([platform isEqualToString:@"iPhone8,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhoneSE;
        return @"iPhone SE (A1662/A1723/A1724)";
    }
    if ([platform isEqualToString:@"iPhone9,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone7;
        return @"iPhone 7 (A1660/A1779/A1780)";
    }
    if ([platform isEqualToString:@"iPhone9,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone7;
        return @"iPhone 7 (A1778)";
    }
    if ([platform isEqualToString:@"iPhone9,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone7Plus;
        return @"iPhone 7 Plus (A1661/A1785/A1786)";
    }
    if ([platform isEqualToString:@"iPhone9,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone7Plus;
        return @"iPhone 7 Plus (A1784)";
    }
    if ([platform isEqualToString:@"iPhone10,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone8;
        return @"iPhone 8 (A1863/A1906/A1907)";
    }
    if ([platform isEqualToString:@"iPhone10,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone8;
        return @"iPhone 8 (A1905)";
    }
    if ([platform isEqualToString:@"iPhone10,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone8Plus;
        return @"iPhone 8 Plus (A1864/A1898/A1899)";
    }
    if ([platform isEqualToString:@"iPhone10,5"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone8Plus;
        return @"iPhone 8 Plus (A1897)";
    }
    if ([platform isEqualToString:@"iPhone10,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhoneX;
        return @"iPhone X (A1865/A1902)";
    }
    if ([platform isEqualToString:@"iPhone10,6"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhoneX;
        return @"iPhone X (A1901)";
    }
    if ([platform isEqualToString:@"iPhone11,8"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhoneXR;
        return @"iPhone XR (A1984/A2105/A2106/A2108)";
    }
    if ([platform isEqualToString:@"iPhone11,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhoneXS;
        return @"iPhone XS (A1920/A2097/A2098/A2100)";
    }
    if ([platform isEqualToString:@"iPhone11,6"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhoneXSMax;
        return @"iPhone XS Max (A1921/A2101/A2102/A2104)";
    }
    if ([platform isEqualToString:@"iPhone11,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhoneXSMax;
        return @"iPhone XS Max ()";
    }
    if ([platform isEqualToString:@"iPhone12,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone11;
        return @"iPhone 11";
    }
    if ([platform isEqualToString:@"iPhone12,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone11Pro;
        return @"iPhone 11 Pro";
    }
    if ([platform isEqualToString:@"iPhone12,5"]) {
        instance.deviceModelsType = DeviceModelsTypeIPhone11ProMax;
        return @"iPhone 11 Pro Max";
    }
    // TODO: iPhone 持续更新 ......
    
#pragma mark - iPod touch
    if ([platform isEqualToString:@"iPod1,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPodTouch;
        return @"iPod touch (A1213)";
    }
    if ([platform isEqualToString:@"iPod2,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPodTouch2;
        return @"iPod touch (2nd generation) (A1288/A1319)";
    }
    if ([platform isEqualToString:@"iPod3,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPodTouch3;
        return @"iPod touch (3rd generation) (A1318)";
    }
    if ([platform isEqualToString:@"iPod4,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPodTouch4;
        return @"iPod touch (4th generation) (A1367)";
    }
    if ([platform isEqualToString:@"iPod5,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPodTouch5;
        return @"iPod touch (5th generation) (A1421/A1509)";
    }
    if ([platform isEqualToString:@"iPod7,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPodTouch6;
        return @"iPod touch (6th generation) (A1574)";
    }
    if ([platform isEqualToString:@"iPod9,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPodTouch7;
        return @"iPod touch (7th generation) (A2178)";
    }
    // TODO: iPod touch 持续更新 ......
    
#pragma mark - iPad mini
    if ([platform isEqualToString:@"iPad2,5"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadMini;
        return @"iPad mini (A1432)";
    }
    if ([platform isEqualToString:@"iPad2,6"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadMini;
        return @"iPad mini (A1454)";
    }
    if ([platform isEqualToString:@"iPad2,7"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadMini;
        return @"iPad mini (A1455)";
    }
    if ([platform isEqualToString:@"iPad4,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadMini2;
        return @"iPad mini 2 (A1489)";
    }
    if ([platform isEqualToString:@"iPad4,5"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadMini2;
        return @"iPad mini 2 (A1490)";
    }
    if ([platform isEqualToString:@"iPad4,6"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadMini2;
        return @"iPad mini 2 (A1491)";
    }
    if ([platform isEqualToString:@"iPad4,7"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadMini3;
        return @"iPad mini 3 (A1599)";
    }
    if ([platform isEqualToString:@"iPad4,8"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadMini3;
        return @"iPad mini 3 (A1600)";
    }
    if ([platform isEqualToString:@"iPad4,9"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadMini3;
        return @"iPad mini 3 (A1601)";
    }
    if ([platform isEqualToString:@"iPad5,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadMini4;
        return @"iPad mini 4 (A1538)";
    }
    if ([platform isEqualToString:@"iPad5,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadMini4;
        return @"iPad mini 4 (A1550)";
    }
    if ([platform isEqualToString:@"iPad11,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadMini5;
        return @"iPad mini (5th generation) (A2133)";
    }
    if ([platform isEqualToString:@"iPad11,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadMini5;
        return @"iPad mini (5th generation) (A2124/A2125/A2126)";
    }
    // TODO: iPad mini 持续更新 ......
    
#pragma mark - iPad
    if ([platform isEqualToString:@"iPad1,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad;
        return @"iPad (A1219/A1337)";
    }
    if ([platform isEqualToString:@"iPad2,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad2;
        return @"iPad 2 (A1395)";
    }
    if ([platform isEqualToString:@"iPad2,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad2;
        return @"iPad 2 (A1396)";
    }
    if ([platform isEqualToString:@"iPad2,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad2;
        return @"iPad 2 (A1397)";
    }
    if ([platform isEqualToString:@"iPad2,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad2;
        return @"iPad 2 (A1395)";
    }
    if ([platform isEqualToString:@"iPad3,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad3;
        return @"iPad (3rd generation) (A1416)";
    }
    if ([platform isEqualToString:@"iPad3,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad3;
        return @"iPad (3rd generation) (A1403)";
    }
    if ([platform isEqualToString:@"iPad3,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad3;
        return @"iPad (3rd generation) (A1430)";
    }
    if ([platform isEqualToString:@"iPad3,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad4;
        return @"iPad (4th generation) (A1458)";
    }
    if ([platform isEqualToString:@"iPad3,5"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad4;
        return @"iPad (4th generation) (A1459)";
    }
    if ([platform isEqualToString:@"iPad3,6"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad4;
        return @"iPad (4th generation) (A1460)";
    }
    if ([platform isEqualToString:@"iPad4,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadAir;
        return @"iPad Air (A1474)";
    }
    if ([platform isEqualToString:@"iPad4,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadAir;
        return @"iPad Air (A1475)";
    }
    if ([platform isEqualToString:@"iPad4,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadAir;
        return @"iPad Air (A1476)";
    }
    if ([platform isEqualToString:@"iPad5,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadAir2;
        return @"iPad Air 2 (A1566)";
    }
    if ([platform isEqualToString:@"iPad5,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadAir2;
        return @"iPad Air 2 (A1567)";
    }
    if ([platform isEqualToString:@"iPad6,7"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro12_9;
        return @"iPad Pro (12.9-inch) (A1584)";
    }
    if ([platform isEqualToString:@"iPad6,8"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro12_9;
        return @"iPad Pro (12.9-inch) (A1652)";
    }
    if ([platform isEqualToString:@"iPad6,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro9_7;
        return @"iPad Pro (9.7-inch) (A1673)";
    }
    if ([platform isEqualToString:@"iPad6,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro9_7;
        return @"iPad Pro (9.7-inch) (A1674/A1675)";
    }
    if ([platform isEqualToString:@"iPad6,11"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad5;
        return @"iPad (5th generation) (A1822)";
    }
    if ([platform isEqualToString:@"iPad6,12"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad5;
        return @"iPad (5th generation) (A1823)";
    }
    if ([platform isEqualToString:@"iPad7,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro2_12_9;
        return @"iPad Pro (12.9-inch) (2nd generation) (A1670)";
    }
    if ([platform isEqualToString:@"iPad7,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro2_12_9;
        return @"iPad Pro (12.9-inch) (2nd generation) (A1671/A1821)";
    }
    if ([platform isEqualToString:@"iPad7,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro10_5;
        return @"iPad Pro (10.5-inch) (A1701)";
    }
    if ([platform isEqualToString:@"iPad7,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro10_5;
        return @"iPad Pro (10.5-inch) (A1709)";
    }
    if ([platform isEqualToString:@"iPad7,5"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad6;
        return @"iPad (6th generation) (A1893)";
    }
    if ([platform isEqualToString:@"iPad7,6"]) {
        instance.deviceModelsType = DeviceModelsTypeIPad6;
        return @"iPad (6th generation) (A1954)";
    }
    if ([platform isEqualToString:@"iPad8,1"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro11;
        return @"iPad Pro (11-inch) (A1980)";
    }
    if ([platform isEqualToString:@"iPad8,2"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro11;
        return @"iPad Pro (11-inch) (A1980)";
    }
    if ([platform isEqualToString:@"iPad8,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro11;
        return @"iPad Pro (11-inch) (A1934)";
    }
    if ([platform isEqualToString:@"iPad8,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro11;
        return @"iPad Pro (11-inch) (A1934)";
    }
    if ([platform isEqualToString:@"iPad8,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro11;
        return @"iPad Pro (11-inch) (A1979)";
    }
    if ([platform isEqualToString:@"iPad8,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro11;
        return @"iPad Pro (11-inch) (A1979)";
    }
    if ([platform isEqualToString:@"iPad8,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro11;
        return @"iPad Pro (11-inch) (A2013)";
    }
    if ([platform isEqualToString:@"iPad8,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro11;
        return @"iPad Pro (11-inch) (A2013)";
    }
    if ([platform isEqualToString:@"iPad8,5"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro3_12_9;
        return @"iPad Pro (12.9-inch) (3rd generation) (A1876)";
    }
    if ([platform isEqualToString:@"iPad8,6"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro3_12_9;
        return @"iPad Pro (12.9-inch) (3rd generation) (A1876)";
    }
    if ([platform isEqualToString:@"iPad8,7"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro3_12_9;
        return @"iPad Pro (12.9-inch) (3rd generation) (A1895)";
    }
    if ([platform isEqualToString:@"iPad8,8"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro3_12_9;
        return @"iPad Pro (12.9-inch) (3rd generation) (A1895)";
    }
    if ([platform isEqualToString:@"iPad8,7"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro3_12_9;
        return @"iPad Pro (12.9-inch) (3rd generation) (A1983)";
    }
    if ([platform isEqualToString:@"iPad8,8"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro3_12_9;
        return @"iPad Pro (12.9-inch) (3rd generation) (A1983)";
    }
    if ([platform isEqualToString:@"iPad8,7"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro3_12_9;
        return @"iPad Pro (12.9-inch) (3rd generation) (A2014)";
    }
    if ([platform isEqualToString:@"iPad8,8"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadPro3_12_9;
        return @"iPad Pro (12.9-inch) (3rd generation) (A2014)";
    }
    if ([platform isEqualToString:@"iPad11,3"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadAir3;
        return @"iPad Air (3rd generation) (A2152)";
    }
    if ([platform isEqualToString:@"iPad11,4"]) {
        instance.deviceModelsType = DeviceModelsTypeIPadAir3;
        return @"iPad Air (3rd generation) (A2123/A2153/A2154)";
    }
    // TODO: iPad 持续更新 ......
    
#pragma mark - iPhone Simulator
    if ([platform isEqualToString:@"i386"])    {
        self.deviceModelsType = DeviceModelsTypeIPhoneSimulator;
        return @"iPhone Simulator";
    }
    
    if ([platform isEqualToString:@"x86_64"])    {
        self.deviceModelsType = DeviceModelsTypeIPhoneSimulator;
        return @"iPhone Simulator";
    }
    
    self.deviceModelsType = DeviceModelsTypeIPhoneNone;
    return @"型号未知";
}

@end
```
