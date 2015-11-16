---
layout: post
title: "WorkKit库"
description: "WorkKit库"
category: iOS
tags: [学习]
---


```
#  pod 'WDWorkKit',:git => 'https://github.com/BaroneX/WDWorkKit.git'
#  pod 'AFNetworking'
#  pod 'SDWebImage'
#  pod 'Masonry'
#  pod 'MBProgressHUD'
#  pod 'MJRefresh'
#  pod 'TTTAttributedLabel'
#  pod 'LKDBHelper'
#  pod 'SVProgressHUD'
#  pod 'MJExtension'
#  pod 'IQKeyboardManager'
#  pod 'DateTools'
```

```
WDWorkKit
├── Assets #资源文件
│   ├── b27_icon_star_gray@2x.png
│   ├── b27_icon_star_yellow@2x.png
│   ├── radio_checked.png
│   └── radio_unchecked.png
└── Classes
    ├── WDControl #control
    │   ├── UIBarButtonItem+WDActionBlock.h
    │   ├── UIBarButtonItem+WDActionBlock.m
    │   ├── UIControl+WDActionBlock.h
    │   ├── UIControl+WDActionBlock.m
    │   ├── UIGestureRecognizer+WDActionBlock.h
    │   ├── UIGestureRecognizer+WDActionBlock.m
    │   ├── WDActionBlockWrapper.h
    │   └── WDActionBlockWrapper.m
    ├── WDFrameWork #基础
    │   ├── NSDate+WDCalendar.h
    │   ├── NSDate+WDCalendar.m
    │   ├── NSString+Addition.h
    │   ├── NSString+Addition.m
    │   ├── Reachability.h
    │   ├── Reachability.m
    │   ├── UIDevice+Addition.h
    │   ├── UIDevice+Addition.m
    │   ├── UIImage+Addition.h
    │   ├── UIImage+Addition.m
    │   ├── WDCoreAnimationEffect.h
    │   ├── WDCoreAnimationEffect.m
    │   ├── WDCountButton.h
    │   ├── WDCountButton.m
    │   ├── WDCycleScrollView.h
    │   ├── WDCycleScrollView.m
    │   ├── WDFrameWork.h
    │   ├── WDJsonKit.h
    │   ├── WDJsonKit.m
    │   ├── WDReachability.h
    │   ├── WDReachability.m
    │   ├── WDSandbox.h
    │   ├── WDSandbox.m
    │   ├── WDSystemInfo.h
    │   ├── WDSystemInfo.m
    │   ├── WDUIConfigDefine.h
    │   ├── WDViewExt.h
    │   └── WDViewExt.m
    ├── WDNetWork #网络组件
    │   ├── WDNetWork.h
    │   └── WDNetWork.m
    ├── WDUI     #UI组件
    │   ├── CWStarRateView
    │   ├── DOPDropDownMenu.h
    │   ├── DOPDropDownMenu.m
    │   ├── ImageLoader
    │   ├── JKAlertDialog
    │   ├── MPNotificationView
    │   ├── PopoverView.h
    │   ├── PopoverView.m
    │   ├── QRadioButton
    │   ├── UIView+Toast.h
    │   └── UIView+Toast.m
    └── WDWorkKit.h	 #头文件

```

```
WDPayKit/ 
├── WDPayConfig.h 	//配置文件
├── WDPayKit.h    	//支付接口
├── WDPayKit.mm   
├── WDPayResult.h 	//交易结果类
├── WDPayResult.m
│   
├── ALPay  			//支付宝
│   ├── AlipaySDK.bundle
│   ├── AlipaySDK.framework
│   ├── WDALPayAdapter.h 
│   └── WDALPayAdapter.m
│   
├── UPPAY 			 //银联
│   ├── UPPayPlugin.h
│   ├── UPPayPluginDelegate.h
│   ├── WDUNPayAdapter.h
│   ├── WDUNPayAdapter.m
│   └── libUPPayPlugin.a
│   
└── WXPay  			//微信
    ├── WDWXPayAdapter.h
    ├── WDWXPayAdapter.m
    ├── WXApi.h
    ├── WXApiObject.h
    ├── libWeChatSDK.a
    └── read_me.txt
```
