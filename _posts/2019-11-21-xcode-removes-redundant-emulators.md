---
layout: post
title: Xcode删除多余的模拟器
date: 2019-11-21
Author: gwl
categories: iOS
tags: [xcode, simulator]
comments: true
---

Xocde会自带一个模拟器，且都是随安装包一起打包的，比如Xcode11的就自带iOS13的模拟器，这个是没办法删除。我们可以在 Xcode/Prefrences/Components 中下载不同版本的模拟器。

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article%20images/2019-11-21-xcode-removes-redundant-emulators/2019-11-21-xcode-removes-redundant-emulators-01.png?raw=true)

下载后的模拟器在目录为 `/资源库/Developer/CoreSimulator/Profiles/Runtimes/` 该文件夹下放置的就是我们下载的不同版本的模拟器,选中你想删除的删除即可

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article%20images/2019-11-21-xcode-removes-redundant-emulators/2019-11-21-xcode-removes-redundant-emulators-02.png?raw=true)
