---
layout: post
title: 使用UIImagePickerController录制视频
date: 2019-11-22
Author: gwl
categories: iOS
tags: [UIImagePickerController]
comments: true
---


导入头文件
```
#import <CoreServices/CoreServices.h>
#import <AVFoundation/AVFoundation.h>
```

代理
```
<UIImagePickerControllerDelegate, UINavigationControllerDelegate>
```

```
- (void)recordVideo {
    UIImagePickerController *picker = [[UIImagePickerController alloc] init];
    if ([UIImagePickerController isSourceTypeAvailable:UIImagePickerControllerSourceTypeCamera]) {
        picker.sourceType = UIImagePickerControllerSourceTypeCamera;
    }
    
    // 设置使用相机的类型
    NSString *mediaType = (__bridge NSString *)kUTTypeMovie;
    picker.mediaTypes = @[mediaType];
    picker.delegate = self;
    // 设置录像的视频质量
    picker.videoQuality = UIImagePickerControllerQualityTypeHigh;
    // 设置最大限制的录制时间
    picker.videoMaximumDuration = 10;
    [self presentViewController:picker animated:YES completion:nil];
}
- (void)imagePickerController:(UIImagePickerController *)picker didFinishPickingMediaWithInfo:(NSDictionary<UIImagePickerControllerInfoKey, id> *)info {
    NSString *mediaType = info[UIImagePickerControllerMediaType];
    NSString *movieType = (__bridge NSString *)kUTTypeMovie;
    
    if ([movieType isEqualToString:mediaType]) {
        NSURL *url = info[UIImagePickerControllerMediaURL];
        
        NSFileManager *fileManager = [NSFileManager defaultManager];
        NSDictionary *dict = [fileManager attributesOfItemAtPath:url.path error:nil];
        
        NSLog(@"大小:%d - 时长:%f", [[dict objectForKey:NSFileSize] intValue] / 1024 / 1024, CMTimeGetSeconds([AVAsset assetWithURL:url].duration));
    }
    [picker dismissViewControllerAnimated:YES completion:nil];
}
- (void)imagePickerControllerDidCancel:(UIImagePickerController *)picker {
    [picker dismissViewControllerAnimated:YES completion:nil];
}
```

使用 `videoMaximumDuration` 设置最大限制的录制时间，录制结束后会弹出 `已停止录像` 的提示信息，可把 `videoMaximumDuration` 属性替换成 `stopVideoCapture` 方法主动停止
