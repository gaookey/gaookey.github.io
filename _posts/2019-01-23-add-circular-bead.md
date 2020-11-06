---
layout: post
title: iOS 图片、文字加圆角
date: 2019-01-23
Author: gwl
categories: iOS
tags: [圆角]
comments: false
toc: true
---

```swift
extension UIView {
    
    enum BorderPosition: Int {
        case top
        case bottom
        case left
        case right
    }
    
    
    /// 圆角边框
    /// - Parameters:
    ///   - maskedCorners: 圆角位置
    ///   - cornerRadius: 圆角大小
    ///   - borderColor: 边框颜色
    ///   - borderWidth: 边框宽度
    func corner(maskedCorners: CACornerMask, cornerRadius: CGFloat, borderColor: UIColor = .clear, borderWidth: CGFloat = 0) {
        
        layer.masksToBounds = true
        layer.cornerRadius = cornerRadius
        layer.borderColor = borderColor.cgColor
        layer.borderWidth = borderWidth
        if maskedCorners != [] {
            layer.maskedCorners = maskedCorners
        }
    }
    
    /// 圆角边框虚线
    /// - Parameters:
    ///   - rect: frame
    ///   - corner: 圆角位置
    ///   - cornerRadius: 圆角大小
    ///   - borderColor: 边框颜色
    ///   - borderWidth: 边框宽度
    ///   - lineDashPattern: 虚线
    func corner(clipRect rect: CGRect, corner: UIRectCorner = .allCorners, cornerRadius: CGFloat = 0, borderColor: UIColor = .clear, borderWidth: CGFloat = 0, lineDashPattern: [NSNumber] = []) {
        
        let path = UIBezierPath(roundedRect: rect, byRoundingCorners: corner, cornerRadii: CGSize(width: cornerRadius, height: cornerRadius))
        
        let maskLayer = CAShapeLayer()
        maskLayer.path = path.cgPath
        layer.mask = maskLayer
        
        let borderLayer = CAShapeLayer()
        borderLayer.path = path.cgPath
        borderLayer.lineWidth = borderWidth * 2
        borderLayer.fillColor = UIColor.clear.cgColor
        borderLayer.strokeColor = borderColor.cgColor
        borderLayer.lineDashPattern = lineDashPattern
        layer.addSublayer(borderLayer)
    }
    
    /// 边框
    /// - Parameters:
    ///   - position: 边框位置
    ///   - borderColor: 边框颜色
    ///   - borderWidth: 边框宽度
    func border(position: [BorderPosition], borderColor: UIColor, borderWidth: CGFloat) {
        
        for p in position {
            let borderLayer = CAShapeLayer()
            borderLayer.backgroundColor = borderColor.cgColor
            layer.addSublayer(borderLayer)
            
            switch p {
            case .top:
                borderLayer.frame = CGRect(x: 0, y: 0, width: frame.width, height: borderWidth)
            case .bottom:
                borderLayer.frame = CGRect(x: 0, y: frame.height - borderWidth, width: frame.width, height: borderWidth)
            case .left:
                borderLayer.frame = CGRect(x: 0, y: 0, width: borderWidth, height: frame.height)
            case .right:
                borderLayer.frame = CGRect(x: frame.width - borderWidth, y: 0, width: borderWidth, height: frame.height)
            }
        }
    }
    
    /// 阴影
    /// - Parameters:
    ///   - color: 阴影颜色
    ///   - offset: 阴影偏移量。（width和height都为0（CGSize.zero），阴影在四周。width为负值，阴影朝左。width为正值，阴影朝右。height为负值，阴影朝上。height为正值，阴影朝下。）
    ///   - radius: 阴影圆角
    ///   - opacity: 阴影透明度
    func shadow(color: UIColor, offset: CGSize, radius: CGFloat, opacity: Float) {
        layer.shadowColor = color.cgColor
        layer.shadowOffset = offset
        layer.shadowRadius = radius
        layer.shadowOpacity = opacity
    }
}
```

### 图片

```objectivec
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

```objectivec
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

```objectivec

UIImageView *imageView = [[UIImageView alloc] initWithFrame:CGRectMake(100, 100, 100, 100)];
imageView.image = [UIImage imageNamed:@"image"];
[self.view addSubview:imageView];

UIBezierPath *path = [UIBezierPath bezierPathWithRoundedRect:imageView.bounds byRoundingCorners:UIRectCornerBottomLeft | UIRectCornerTopRight cornerRadii:CGSizeMake(28, 28)];
CAShapeLayer *layer = [CAShapeLayer layer];
layer.path = path.CGPath;
imageView.layer.mask  = layer;
```

### 文字

```objectivec
UILabel *lable = [[UILabel alloc] initWithFrame:CGRectMake(100, 100, 100, 100)];
lable.text = @"测试文本";
lable.backgroundColor = [UIColor cyanColor];
[self.view addSubview:lable];

UIBezierPath *path = [UIBezierPath bezierPathWithRoundedRect:lable.bounds byRoundingCorners:UIRectCornerBottomLeft | UIRectCornerTopRight cornerRadii:CGSizeMake(28, 28)];
CAShapeLayer *layer = [CAShapeLayer layer];
layer.path = path.CGPath;
lable.layer.mask  = layer;
```


### UIBezierPath

```swift
class SpView: UIView {
    
    override init(frame: CGRect) {
        super.init(frame: frame)
        
        backgroundColor = .clear
    }
    
    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
    override func draw(_ rect: CGRect) {
        
        let points = [
            CGPoint(x: bounds.width * 0.5 - 9, y: bounds.height - 8),
            CGPoint(x: bounds.width * 0.5 + 9, y: bounds.height - 8),
            CGPoint(x: bounds.width * 0.5, y: bounds.height)
        ]
        
        let path = UIBezierPath(roundedRect: CGRect(x: 0, y: 0, width: bounds.width, height: bounds.height - 8), cornerRadius: 16)
        path.move(to: points[0])
        for i in 1..<points.count {
            path.addLine(to: points[i])
        }
        
        UIColor.white.set()
        path.stroke()
        path.fill()
        
        let shadowPath = UIBezierPath(roundedRect: CGRect(x: 0, y: 0, width: bounds.width, height: bounds.height - 8), cornerRadius: 16)
        layer.shadowColor = UIColor.red.cgColor
        layer.shadowOffset = .zero
        layer.shadowRadius = 12
        layer.shadowOpacity = 1
        
        shadowPath.move(to: points[0])
        for i in 1..<points.count {
            shadowPath.addLine(to: points[i])
        }
        
        layer.shadowPath = shadowPath.cgPath
    }
}
```