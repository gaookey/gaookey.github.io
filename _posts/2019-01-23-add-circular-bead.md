---
layout: post
title: iOS 图片、文字加圆角
date: 2019-01-23
Author: gwl
categories: iOS
tags: [圆角]
comments: true
toc: true
---

### 图片

```objective-c
#import "UIImageView+CircleImage.h"

@implementation UIImageView (CircleImage)

- (void)circleImage:(CGFloat)cornerRadius {
    UIGraphicsBeginImageContextWithOptions(self.bounds.size, NO, 1.0);
    [[UIBezierPath bezierPathWithRoundedRect:self.bounds cornerRadius:cornerRadius] addClip];
    [self.image drawInRect:self.bounds];
    self.image = UIGraphicsGetImageFromCurrentImageContext();
    UIGraphicsEndImageContext();
}

- (void)circleImage:(CGFloat)cornerRadius rectCorner:(UIRectCorner)rectCorner {

    self.contentMode = UIViewContentModeScaleAspectFill;
    
    CAShapeLayer *shapeLayer = [CAShapeLayer layer];
    shapeLayer.backgroundColor = [UIColor clearColor].CGColor;
    shapeLayer.path = [UIBezierPath bezierPathWithRoundedRect:self.bounds byRoundingCorners:rectCorner cornerRadii:CGSizeMake(cornerRadius, cornerRadius)].CGPath;
    self.layer.masksToBounds = YES;
    self.layer.mask = shapeLayer;
    shapeLayer.frame = self.layer.bounds;
}

@end
```

```objective-c
#import "UIImage+CircleImage.h"

@implementation UIImage (CircleImage)

/**
 contentMode = UIViewContentModeScaleToFill
 */
- (UIImage *)circleImage {
    
    UIGraphicsBeginImageContextWithOptions(self.size, NO, 0.0);
    CGContextRef ctx = UIGraphicsGetCurrentContext();
    CGRect rect = CGRectMake(0, 0, self.size.width, self.size.height);
    CGContextAddEllipseInRect(ctx, rect);
    CGContextClip(ctx);
    [self drawInRect:rect];
    UIImage *image = UIGraphicsGetImageFromCurrentImageContext();
    UIGraphicsEndImageContext();
    return image;
}

@end
```

### 文字

```objective-c
UILabel *lable = [[UILabel alloc] initWithFrame:CGRectMake(100, 100, 100, 100)];
lable.text = @"测试文本";
lable.backgroundColor = [UIColor cyanColor];
[self.view addSubview:lable];

UIBezierPath *path = [UIBezierPath bezierPathWithRoundedRect:image.bounds byRoundingCorners:UIRectCornerBottomLeft | UIRectCornerTopRight cornerRadii:CGSizeMake(28, 28)];
CAShapeLayer *layer = [CAShapeLayer layer];
layer.path = path.CGPath;
image.layer.mask  = layer;
```
