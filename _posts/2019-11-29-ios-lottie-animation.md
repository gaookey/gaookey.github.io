---
layout: post
title: iOS - Lottie动画
date: 2019-11-29
Author: gwl
categories: iOS
tags: [lottie, lottiefiles]
comments: true
---



[LottieFiles 网站](https://lottiefiles.com/) 下载动画的 LottieFile  JSON 文件添加到项目中

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-11-29-ios-lottie-animation/2019-11-29-ios-lottie-animation-01.png?raw=true)

导入 **[lottie-ios](https://github.com/airbnb/lottie-ios)** 库，objective-c项目添加版本号2.5

```objective-c
pod 'lottie-ios' , '~> 2.5'
```

导入头文件 `#import <Lottie/Lottie.h>` 即可使用

```objective-c
LOTAnimationView *animation = [[LOTAnimationView alloc] initWithFrame:CGRectMake(200, 200, 200, 200)];
animation.animation = @"11803-send-button";
[self.view addSubview:animation];
```

###### 简单几个属性

播放动画

`play`

暂停动画，方法playWithCompletion将被调用

`pause`

停止动画，方法playWithCompletion将被调用

`stop`

动画速度，倍数

`animationSpeed`

是否循环播放，默认NO

`loopAnimation`

设置动画从0 - 1的进度。如果动画正在播放，它将停止，方法playWithCompletion将被调用

`animationProgress`