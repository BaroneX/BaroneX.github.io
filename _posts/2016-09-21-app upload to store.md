---
layout: post
title: "[转]iOS-最全的App上架教程"
description: "iOS-App上架"
category: iOS
tags: [Tips]
---

[转自][iOS-最全的App上架教程](http://www.jianshu.com/p/cea762105f7c#)

准备

开发者账号
完工的项目
上架步骤

一、创建App ID

二、创建证书请求文件 （CSR文件）

三、创建发布证书 （CER）

四、创建Provisioning Profiles配置文件 （PP文件）

五、在App Store创建应用

六、打包上架

一、创建App ID

1.打开苹果开发者官网，点击“Account”登录会员中心。

 ![image](/assets/20160921/1.png)

 ![image](/assets/20160921/2.png)

 ![image](/assets/20160921/3.png)

2.填写信息创建app ID

 ![image](/assets/20160921/4.png)

点击+创建ID

 ![image](/assets/20160921/5.png)

 ![image](/assets/20160921/6.png)



二、创建证书请求文件（CSR文件）

CRS文件主要用于 绑定你的电脑的

1 点开LaunchPad，在其他中找到打开钥匙串访问

 ![image](/assets/20160921/7.png)


2 点击电脑左上角的钥匙串访问–证书助理–从证书颁发机构请求证书

 ![image](/assets/20160921/8.png)


3 出现如下界面，选择存储到磁盘，点击继续

 ![image](/assets/20160921/9.png)


4 选择存储到桌面，存储

 ![image](/assets/20160921/10.png)


5 点击完成

 ![image](/assets/20160921/11.png)


6 在桌面上看到下面的文件，证书请求文件完成

 ![image](/assets/20160921/12.png)


三、创建发布证书 (CER文件)

1 找到Certificates ，点击All，然后点击右上角 + 号

 ![image](/assets/20160921/13.png)


2 点击App Store and Ad Hoc

 ![image](/assets/20160921/14.png)


发布证书和开发者证书需要分别创建，操作两次，开发者证书用于真机调试，发布证书用于提交到AppStore。

3. 点击Continue

 ![image](/assets/20160921/15.png)


4. 点击Continue

 ![image](/assets/20160921/16.png)


5. 点击choose File.. 选择创建好的证书请求文件：CertificateSigningRequest.certSigningRequest 文件，点击Generate

 ![image](/assets/20160921/17.png)


6. 点击Download下载创建好的发布证书（cer后缀的文件），然后点击Done，你创建的发布证书就会存储在帐号中。

 ![image](/assets/20160921/18.png)


7. 双击安装。如果安装不上，可以直接将证书文件拖拽到钥匙串访问的列表中

重点: 一般一个开发者帐号创建一个发布证书就够了，如果以后需要在其他电脑上上架App，只需要在钥匙串访问中创建p12文件，把p12文件安装到其他电脑上。这相当于给予了其他电脑发布App的权限。

四、创建Provisioning Profiles文件

1.找到Provisioning Profiles ，点击All，然后点击右上角 + 号

 ![image](/assets/20160921/19.png)


2.选择App Store，点击Continue

 ![image](/assets/20160921/20.png)


该流程也需要进行两次，分别创建开发用的PP证书和发布的PP证书。

3.在App ID 这个选项栏里面找到你刚刚创建的：App IDs（Bundle ID） 类型的套装，点击Continue

 ![image](/assets/20160921/21.png)


4.选择你刚创建的发布证书（或者生成p12文件的那个发布证书），点击Continue

 ![image](/assets/20160921/22.png)


5.在Profile Name栏里输入一个名字（这个是PP文件的名字，可随便输入，在这里我用工程名字，便于分别），然后点击Generate

 ![image](/assets/20160921/23.png)


注意：wildCard格式的证书没有推送，PassCard等服务的应用，慎重选择。因为PP证书的开发者证书需要真机调试，所以我们需要绑定真机，这里因为之前添加过一些设备，所以这里就可以直接全选添加，如果没有的话，需要将真机的udid复制出来在此添加。在发布PP文件中，是没有这一步的。

6.Download生成的PP文件，然后点击Done

 ![image](/assets/20160921/24.png)


双击就添加到Xcode中，这样在真机调试或者发布时，就可以分别有不同的PP证书与其对应。其实可以不用下载保存

五、在App Store创建应用

1、回到Account，点击iTunes Connect

 ![image](/assets/20160921/25.png)


2、点击我的App

 ![image](/assets/20160921/26.png)

3、点击新建 iOSApp

 ![image](/assets/20160921/27.png)


4、依次按提示填入对应信息，然后点击创建

 ![image](/assets/20160921/28.png)

5、依次把不同尺寸的App截图拉入到对应的里面

 ![image](/assets/20160921/29.png)


6、填入App简介

 ![image](/assets/20160921/30.png)


7、按提示依次输入

 ![image](/assets/20160921/31.png)


此时这个构建版本还没有生成，我们先把基本信息填写完毕，然后再进入Xcode中把项目打包发送到过来。注意：填写完一定要点击右上角的保存。

 ![image](/assets/20160921/32.png)


不要忘记填写测试账号，否则会被拒的，而且一定要跟服务器同事说好，不要删除测试账号，否则同样被拒（联系号码 一定要+ 86 如：+86 13720329661）

六、打包上架

在Xcode中打包工程找到你刚刚下载的发布证书（后缀为.cer）或者p12文件，和PP文件，双击，看起来没反应，但是他们已经加入到你的钥匙串中。如果之前步骤已操作过，可省略此步。

1、打开Xcode，配置项目环境，点击+可以选择Add Apple ID；点击View Details可以查看该Apple Id下的Certificates和Provisioning Profile证书文件，在这里你可以点击下载。在项目Targets下的Identity中，Team选择对应的Apple ID 即可。

 ![image](/assets/20160921/33.png)


特别注意： 这里填写的Apple ID 不是你自己手机上创建的Apple ID 一定要是 开发者账号的 账号和密码 （~QAQ~ 我就在这里被坑过）

2、选择模拟器为iOS Device，按照下图提示操作

 ![image](/assets/20160921/34.png)


3、修改.plist文件，两个.plist文件都要修改

 ![image](/assets/20160921/35.png)


4、Archive在线打包，在真机状态下选择Product——>Archive，如果不是真机状态下，Archive会是灰色不可用的)。

 ![image](/assets/20160921/36.png)


5、打包之后会生成一个 ipa文件 ，然后返回我的App~~在构建版本处，点击Application Loader 就会将其下载下来，然后通过该软件把ipa文件上传到 appstore上。

 ![image](/assets/20160921/37.png)


 ![image](/assets/20160921/38.png)


 ![image](/assets/20160921/39.png)


 ![image](/assets/20160921/40.png)


打包过程中 会出现的问题

 ![image](/assets/20160921/41.png)


解决方案：iOS- 打包时 UUID出错的解决方案

application Loader 上传出现的错误

 ![image](/assets/20160921/42.png)


6.发送成功后返回到我的App，刷新页面，在构建版本处就会有个 + 号，点击 + 号把发送过来的程序添加上去就行了

7.提交审核


