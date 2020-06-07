---
layout: post
title: iOS - js oc相互调用
date: 2017-11-28
Author: gwl
categories: iOS
tags: [js]
comments: true
toc: true
---


##### 首先导入 `JavaScriptCore.framework` 框架

##### .h

```
#import <UIKit/UIKit.h>
#import <Foundation/Foundation.h>
#import <JavaScriptCore/JavaScriptCore.h>

@protocol ServerJSProtocol <JSExport>

// 微信登录
- (void)wxLogin;
// 忘记密码
- (void)toForget;
// 去注册
- (void)toReg;

// 登录
- (BOOL)userLogin:(BOOL)nc_vok :(NSString *)csessionid :(NSString *)sig :(NSString *)token :(NSString *)scene :(NSString *)tx_Usermobilenum :(NSString *)tx_UserPassword;

@end

@interface ServerJS : NSObject <ServerJSProtocol>

@end
```

##### .m

```
#import "ServerJS.h"

@implementation ServerJS

- (void)wxLogin {
    
}
- (void)toForget {
    
}
- (void)toReg {
    
}
- (BOOL)userLogin:(BOOL)nc_vok :(NSString *)csessionid :(NSString *)sig :(NSString *)token :(NSString *)scene :(NSString *)tx_Usermobilenum :(NSString *)tx_UserPassword {
    return YES;
}

@end
```

##### 使用

```
- (void)webViewDidFinishLoad:(UIWebView *)webView {
    JSContext *context = [webView valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];

    ServerJS *js = [[ServerJS alloc] init];
    context[@"mobileObj"] = js;
}
```

> 方法名 和 mobileObj 必须和js里面的一样
>
> > 附上js部分代码

```
document.getElementById("bt_login").onclick = function(){
    if (!mobileObj.userLogin(nc_vok,
                             document.getElementById('csessionid').value,
                             document.getElementById('sig').value,
                             document.getElementById('token').value,
                             document.getElementById('scene').value,
                             document.getElementById('tx_Usermobilenum').value,
                             document.getElementById('tx_UserPassword').value)) {
        resetAliyunAfs();
    }
};

document.getElementById("wxlogin").onclick = function(){
    mobileObj.wxLogin();
};

document.getElementById("bt_forget").onclick = function(){
    mobileObj.toForget();
};

document.getElementById("bt_reg").onclick = function(){
    mobileObj.toReg();
};
```
