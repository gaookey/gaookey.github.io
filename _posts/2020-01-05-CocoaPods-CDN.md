---
layout: post
title: CDN: trunk Repo update failed - 3 error(s):
date: 2020-01-05
Author: gwl
categories: iOS
tags: [CDN, CocoaPods]
comments: true
toc: true
---


### 环境

CocoaPods 1.8.4

Xcode 11.3

macOS 10.15.2

### 问题

`pod install` 安装库的时候出现了以下问题

> [!] CDN: trunk Repo update failed - 3 error(s):
> CDN: trunk URL couldn't be downloaded: https://raw.githubusercontent.com/CocoaPods/Specs/master/Specs/a/7/5/AFNetworking/1.0/AFNetworking.podspec.json, error: Failed to open TCP connection to raw.githubusercontent.com:443 (Connection refused - connect(2) for "raw.githubusercontent.com" port 443)
> CDN: trunk URL couldn't be downloaded: https://raw.githubusercontent.com/CocoaPods/Specs/master/Specs/a/7/5/AFNetworking/2.6.0/AFNetworking.podspec.json, error: Failed to open TCP connection to raw.githubusercontent.com:443 (Connection refused - connect(2) for "raw.githubusercontent.com" port 443)
> CDN: trunk URL couldn't be downloaded: https://raw.githubusercontent.com/CocoaPods/Specs/master/Specs/a/7/5/AFNetworking/3.2.0/AFNetworking.podspec.json, error: Failed to open TCP connection to raw.githubusercontent.com:443 (Connection refused - connect(2) for "raw.githubusercontent.com" port 443)


关于CDN的引入请看[CocoaPods官方介绍：http://blog.cocoapods.org/CocoaPods-1.8.0-beta/](http://blog.cocoapods.org/CocoaPods-1.8.0-beta/)

### 我的解决方案

##### 第一步： `Podfile` 中添加 `source 'https://github.com/CocoaPods/Specs.git'`

```
source 'https://github.com/CocoaPods/Specs.git'

platform:ios,'10.0'

#inhibit_all_warnings!
#use_frameworks!

target 'test' do

pod 'GWLCustomButton'

end
```

##### 第二步： `pod repo list` 查看一下源列表，显示 `cocoapods` 和 `trunk`

##### 第三步： `pod repo remove trunk` 移除 `trunk` 源，移除 `trunk` 源后只剩 `cocoapods` 源

```
cocoapods
- Type: git (master)
- URL:  https://github.com/CocoaPods/Specs.git
- Path: /Users/gwl/.cocoapods/repos/cocoapods

1 repo
```

##### 第四步： 执行 `pod install` 安装，会显示：Cloning spec repo `cocoapods` from `https://github.com/CocoaPods/Specs.git` 信息，接下来就是漫长的等待，很漫长...，然后安装成功