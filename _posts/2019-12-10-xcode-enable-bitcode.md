---
layout: post
title: iOS - You must rebuild it with bitcode enabled (Xcode setting ENABLE_BITCODE), obtain an updated library from the vendor, or disable bitcode for this target.
date: 2019-12-10
Author: gwl
categories: iOS
tags: [bitcode enabled]
comments: true
---


#### 错误显示

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-12-10-xcode-enable-bitcode/2019-12-10-xcode-enable-bitcode-01.png?raw=true)

#### 问题分析

从上述的错误中应该可以看出，这是因为一个第三方的库不兼容，我的工程中开启了 ENABLE_BITCODE （应该是升级之后自动转换的），而这个第三方的库在编译的时候没有 enable bitcode，所以导致上诉问题。

#### 解决办法

##### 1

换成 enable bitcode 的第三方库

##### 2 

Build Setting -> Enable Bitcode 设置为 NO

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-12-10-xcode-enable-bitcode/2019-12-10-xcode-enable-bitcode-02.png?raw=true)
