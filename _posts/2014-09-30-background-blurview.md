---
layout: post
title: "支付宝后台模糊效果"
description: "支付宝后台模糊效果"
category: iOS
tags: [Tips]
---



#支付宝后台模糊效果
```
- (void)applicationDidEnterBackground:(UIApplication *)application
{
    //进入后台添加模糊视图
    blurView = [WDBlurView getBlurView];
    [self.window addSubview:blurView];
    
}

-(void)application:(UIApplication *)application performFetchWithCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler{
    
    completionHandler(UIBackgroundFetchResultNewData);
    
}

- (void)applicationWillEnterForeground:(UIApplication *)application
{
    //进入前端删除视图
    [blurView removeFromSuperview];
    
}
```
