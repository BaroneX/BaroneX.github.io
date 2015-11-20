---
layout: post
title: "清除Xcode mobileprovision文件"
description: "清除Xcode mobileprovision文件"
category: iOS
tags: [Tips]
---

如何清除xcode里面的mobileprovision文件

通过终端进行删除 进入Profiles目录

	cd ~/Library/MobileDevice/Provisioning\ Profiles/

然后删除里面所有的mobileprovision文件

	rm *.mobileprovision

然后打开
	
	Xcode->preferences->Accounts->View Details...
	下载相应的Profiles