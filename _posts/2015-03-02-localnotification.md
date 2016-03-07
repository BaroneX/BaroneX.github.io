---
layout: post
title: "本地通知"
description: "本地通知"
category: iOS
tags: [学习]
---


#本地通知

 ```
 //
//  AppDelegate.m
//  Map
//
//  Created by Blake on 15/3/2.
//  Copyright (c) 2015年 Blake. All rights reserved.
//

#import "AppDelegate.h"

@interface AppDelegate ()

@end

@implementation AppDelegate


- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
    
    
    //ios8以上必须要申请通知,ios8以下不需要申请直接可以添加通知
    //ios8以上关闭通知中心,不会接到本地通知,
    //ios8以下本地通知关闭不了.
    
    if ([[[UIDevice currentDevice]systemVersion]floatValue]<8.0) {
        //小于8直接添加本地通知
        [self addLocalNotification];

    }else{
        //8以上需要授权
        //如果已经获得发送通知的授权则创建本地通知，否则请求授权(注意：如果不请求授权在设置中是没有对应的通知设置项的，也就是说如果从来没有发送过请求，即使通过设置也打不开消息允许设置)
    if ([[UIApplication sharedApplication]currentUserNotificationSettings].types!=UIUserNotificationTypeNone) {
        [self addLocalNotification];
    }else{
        //申请本地通知的授权
        [[UIApplication sharedApplication]registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeAlert|UIUserNotificationTypeBadge|UIUserNotificationTypeSound  categories:nil]];
    }
    }
    
    
    
    return YES;
}
#pragma mark 调用过用户注册通知方法之后执行（也就是调用完registerUserNotificationSettings:方法之后执行）
-(void)application:(UIApplication *)application didRegisterUserNotificationSettings:(UIUserNotificationSettings *)notificationSettings{
    if (notificationSettings.types!=UIUserNotificationTypeNone) {
        [self addLocalNotification];
    }
}

#pragma mark 进入前台后设置消息信息
-(void)applicationWillEnterForeground:(UIApplication *)application{
    [[UIApplication sharedApplication]setApplicationIconBadgeNumber:0];//进入前台取消应用消息图标
}

#pragma mark 添加本地通知
-(void)addLocalNotification{
    
    //定义本地通知对象
    UILocalNotification *notification=[[UILocalNotification alloc]init];
    //设置调用时间
    notification.fireDate=[NSDate dateWithTimeIntervalSinceNow:3.0];//通知触发的时间，10s以后
    notification.repeatInterval=2;//通知重复次数
    notification.timeZone = [NSTimeZone localTimeZone];
    notification.repeatCalendar=[NSCalendar currentCalendar];//当前日历，使用前最好设置时区等信息以便能够自动同步时间
    //NSCalendarUnitDay设置每天重复
    
    //设置通知属性
    notification.alertBody=@"通知内容";
    notification.applicationIconBadgeNumber=1;//图标右上角数字
    notification.alertAction=@"打开应用"; //锁屏界面的滑动动作提示
//    notification.alertLaunchImage=@"1";//通过点击通知打开应用时的启动图片,这里使用程序启动图片
    notification.soundName=UILocalNotificationDefaultSoundName;//收到通知时播放的声音，默认消息声音
//    notification.soundName=@"msg.caf";//通知声音（需要真机才能听到声音）
    
    //设置用户信息
    notification.userInfo=@{@"keyId":@1,@"KeyName":@"x"};//绑定到通知上的其他附加信息
    
    //调用通知
//    [[UIApplication sharedApplication] presentLocalNotificationNow:notification];
    [[UIApplication sharedApplication] scheduleLocalNotification:notification];

}

//本地通知调用后在前端或者是进入前端时调用
-(void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification{
    //打开应用时调用
    NSLog(@"%@,%@,%@",notification.userInfo,notification.alertBody,notification.alertAction);

}
#pragma mark 移除本地通知，在不需要此通知时记得移除
-(void)removeNotification{
    
    NSArray* notiArray = [[UIApplication sharedApplication]scheduledLocalNotifications];
    
    if (notiArray) {
        
        for (UILocalNotification* local in notiArray) {
            //根据定义的字典信息找到对应的通知取消
            NSLog(@"%@,%@,%@",local.userInfo,local.alertBody,local.alertAction);

            [[UIApplication sharedApplication]cancelLocalNotification:local];
        }
    }
    
    //删除所有通知
//    [[UIApplication sharedApplication] cancelAllLocalNotifications];
}
@end
```