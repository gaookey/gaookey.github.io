---
layout: post
title: iOS cocoapods/pod
date: 2018-09-29
Author: gwl
categories: iOS
tags: [cocoapods]
comments: false
toc: true
---

```objectivec
platform :ios, '9.0' #版本

use_frameworks! #OC和swift混编时添加

inhibit_all_warnings! #消除CocoaPods警告

target ‘test’ do

  pod 'FMDB'
  pod 'AFNetworking', '~> 3.1.0'
  pod 'ReactiveCocoa', '~> 2.1.8', :inhibit_warnings => true #开启ReactiveCocoa警告，否则ReactiveCocoa编译不过

end
```

把Podfile内全部的库更新重新安装
```objectivec
pod install
```

更新指定第三方库
```objectivec
pod update 库名
```

该命令只安装新添加的库，已更新的库忽略
```objectivec
pod install --verbose --no-repo-update
```

该命令只更新指定的库，其它库忽略
```objectivec
pod update 库名--verbose --no-repo-update
```