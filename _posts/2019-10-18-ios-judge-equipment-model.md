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


#### 判断型号

> [https://www.theiphonewiki.com/wiki/Models#cite_note-china-1](https://www.theiphonewiki.com/wiki/Models#cite_note-china-1)

##### Swift

```swift
var systemInfo = utsname()
uname(&systemInfo)

let machineMirror = Mirror(reflecting: systemInfo.machine)
let identifier = machineMirror.children.reduce("") { identifier, element in
    guard let value = element.value as? Int8, value != 0 else {return identifier}
    return identifier + String(UnicodeScalar(UInt8(value)))
}
```



##### OC

**第一种方法**

```objective-c
// 导入头文件
#include <sys/sysctl.h>
```

```objective-c
size_t size;
int nR = sysctlbyname("hw.machine", NULL, &size, NULL, 0);
char *machine = (char *)malloc(size);
nR = sysctlbyname("hw.machine", machine, &size, NULL, 0);
NSString *platform = [NSString stringWithCString:machine encoding:NSUTF8StringEncoding];
free(machine);
```

**第二种方法**

```objective-c
// 导入头文件
#include <sys/utsname.h>
```

```objective-c
struct utsname systemInfo;
uname(&systemInfo);
NSString *deviceString = [NSString stringWithCString:systemInfo.machine encoding:NSUTF8StringEncoding];
```



#### [SPDeviceModels](https://github.com/mouos/SPDeviceModels)

部分代码如下，最新代码移步 [github](https://github.com/mouos/GWLDeviceModels)

```swift
import UIKit

enum DeviceModelsType {
    case Unknown
    
    case Simulator
    
    ...
    
    case IPhone12ProMax
    
    ...
    
    case IPodTouch_7th
    
    ...
    
    case IPadPro_inch12_9_4th
    
    ...
    
    case IPadAir_4th
}

class SPDeviceModels {
    
    static let shared = SPDeviceModels()
    
    var model = (DeviceModelsType.Unknown, "Unknown")
    
    private init() {
        
        model = model(id: identifier())
    }
}

extension SPDeviceModels {
    
    private func model(id: String) -> (type: DeviceModelsType, string: String) {
        
        switch id {
        
        // MARK: - iPad
        
        ...
        
        case "iPad11,7":
            return (.IPad_8th, "iPad (8th generation) (A2428/A2429/A2430)")
            
            
            // MARK: - iPad Air
            
            ...
            
        case "iPad13,2":
            return (.IPadAir_4th, "iPad Air (4th generation) (A2324/A2072)")
            
            
            // MARK: - iPad Pro
            
            ...
            
        case "iPad8,12":
            return (.IPadPro_inch12_9_4th, "iPad Pro (12.9-inch) (4th generation) (A2069/A2232/A2233)")
            
            
            // MARK: - iPad mini
            
            ...
            
        case "iPad11,2":
            return (.IPadMini_5th, "iPad mini (5th generation) (A2124/A2125/A2126)")
            
            
            // MARK: - iPhone
            
            ...
            
        case "iPhone13,4":
            return (.IPhone12ProMax, "iPhone 12 Pro Max (A2342)")
            
            
            // MARK: - iPod touch
            
            ...
            
        case "iPod9,1":
            return (.IPodTouch_7th, "iPod touch (7th generation) (A2178)")
            
            
        // MARK: - Simulator
        case "i386", "x86_64":
            return (.Simulator, "Simulator")
            
        default:
            return (.Unknown, "Unknown")
        }
    }
}

extension SPDeviceModels {
    
    private func identifier() -> String {
        
        var systemInfo = utsname()
        uname(&systemInfo)
        
        let machineMirror = Mirror(reflecting: systemInfo.machine)
        let identifier = machineMirror.children.reduce("") { identifier, element in
            guard let value = element.value as? Int8, value != 0 else {return identifier}
            return identifier + String(UnicodeScalar(UInt8(value)))
        }
        
        return identifier
    }
}
```




> 最后更新日期 2020-11-06