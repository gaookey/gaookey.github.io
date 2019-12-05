---
layout: post
title: iOS - 图片拉伸
date: 2016-12-30
Author: gwl
categories: iOS
tags: [拉伸]
comments: true
---

### 1

```
UIImageView *imageView = [[UIImageView alloc] initWithFrame:CGRectMake(80, 320, 180, 40)];
[self.view addSubview:imageView];

UIImage *image = [UIImage imageNamed:@"QQ20161025-0"];

// 设置上左下右边距
CGFloat topMode= image.size.height * 0.5;
CGFloat leftMode= image.size.width * 0.5;
CGFloat bottomMode= image.size.height * 0.5;
CGFloat rightMode= image.size.width * 0.5;

/*
 拉伸图片
 UIImageResizingModeStretch：拉伸模式，通过拉伸UIEdgeInsets指定的矩形区域来填充图片
 UIImageResizingModeTile：默认 平铺模式，通过重复显示UIEdgeInsets指定的矩形区域来填充图片
 */
image = [image resizableImageWithCapInsets:UIEdgeInsetsMake(topMode, leftMode, bottomMode, rightMode) resizingMode:UIImageResizingModeStretch];

/*
 ios 5.0 之前方法
 计算左边和顶部宽度，自动计算中间 1*1 像素拉伸
 image = [image stretchableImageWithLeftCapWidth:leftMode topCapHeight:topMode];
 */
imageView.image = image;
```

### 2

```
+ (UIImage *)resizableImage:(NSString *)name {
    UIImage *image = [self imageNamed:name];
    return [image stretchableImageWithLeftCapWidth:image.size.width * 0.5 topCapHeight:image.size.height *0.5];
}
```

### 3

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2016-12-30-ios-image-stretch/2016-12-30-ios-image-stretch-01.png?raw=true)
