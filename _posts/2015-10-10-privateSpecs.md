---
layout: post
title: "创建私有podspec库"
description: "私有podspec库"
category: iOS
tags: [学习]
---

#创建私有podspec库

1.远程Specs库添加到本地 .cocospod中

	pod repo add WDSpecs https://github.com/BaroneX/WDSpecs.git

2.创建工程(已有工程新建Spec文件)

	pod lib create WDWorkKit (pod spec create specName)

3.修改工程 打开工程的spec文件,然后验证,根据提示修改代码和spec文件

	pod lib lint
	
4.验证成功后代码push到远端,创建一个tag x.x.x(和podspec文件中描述的一致),push到github

	$ git tag '1.0.0'
	$ git push --tags
	$ git push origin master
	
5.在WDWorkKit.podspec目录下,执行命令,把podSpec推送到本地和远端私有pod仓库
	
	 pod repo push WDSpecs WDWorkKit.podspec
	 
#更新维护
1.更新代码,修改podspec文件

2.验证执行

	pod lib lint

3.编辑完成之后，podupdate 验证无误后推送到远程,并打上新的tag,最后再次使用pod lib lint验证编辑好的podsepc文件，没有自身的WARNING或者ERROR之后，就可以再次提交到Spec Repo中了，命令跟之前是一样的

	pod repo push WTSpecs PodTestLibrary.podspec
		
#使用
	
	source 'https://github.com/BaroneX/WDSpecs.git' #添加私有pod仓库地址
	source'https://github.com/CocoaPods/Specs.git' #cocoaPods地址
	platform :ios, '7.0'
	# Uncomment this line if you're using Swift
	# use_frameworks!
	
	target 'testPod' do
	    pod 'WDWorkKit'
	    或
	    pod 'WDWorkKit',:git => 'https://github.com/BaroneX/WDWorkKit.git'
	end