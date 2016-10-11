---
layout: post
title: "[转]iOS-最全的真机测试教程"
description: "iOS-最全的真机测试教程"
category: iOS
tags: [Tips]
---

[转自][iOS-最全的真机测试教程](http://www.jianshu.com/p/c8e86f62687a)

###准备
* 开发者账号
>自从Xcode7 出来之后，一般的真机测试不需要 开发者账号，也就不需要看这篇教程，只有app具有 “推送”等功能的时候，要真机测试就必须要开发者账号和设置证书。苹果只是让你体验一下它的基本功能，要深入还是要花钱的。

* 待测试的项目

---

###真机测试步骤

* 一、创建App ID
* 二、创建证书请求文件 （CSR文件）
* 三、根据CSR创建开发者证书(CER)(开发、测试用的Develope证书）
* 四、添加设备（Devices）
* 五、根据Devices创建Provisioning Profiles配置文件 （PP文件）
* 六、设置Xcode 然后真机调试

---
###重点

* 使用P12 文件 使多台Mac进行真机调试(或者发布) 【重点】

---

###一、创建App ID
* 1.打开苹果开发者网，点击“Account”登录会员中心。
 
 ![image](/assets/20160921-2/1.png)
 
 ![image](/assets/20160921-2/2.png)
 
 ![image](/assets/20160921-2/3.png)


* 2.填写信息创建app ID

 ![image](/assets/20160921-2/4.png)
 
 点击+创建ID

---

 ![image](/assets/20160921-2/5.png)
 
 ![image](/assets/20160921-2/6.png)


>第一个选项：明确的app id 与项目中的Bundle Identifier相对应
如果你打算将应用程序中加入Game Center，或在应用中使用应 用内购买，进行数据保护，使用iCloud，或者想要给你的应用程序一个唯一的配置文件，你就必须申请Explicit App ID。

>第二个选项：通用app id可以在所有不需要明确id的app中使用
淘宝上卖的真机调试证书就是这个

 ![image](/assets/20160921-2/7.png)

 ![image](/assets/20160921-2/8.png)

 ![image](/assets/20160921-2/9.png)



###二、创建证书请求文件（CSR文件)

创建CSR文件请看《iOS-最全的App上架教程》的第二点这里就不多说了

###三、根据CSR创建开发者证书(CER)

####1、 找到Certificates ，点击All，然后点击右上角 + 号

 ![image](/assets/20160921-2/10.png)


####2 、 点击Developement中的iOS App Developement选项

 ![image](/assets/20160921-2/11.png)


####3. 点击Continue 

 ![image](/assets/20160921-2/12.png)

####4. 点击Continue 

 ![image](/assets/20160921-2/13.png)

####5. 点击choose File.. 选择创建好的证书请求文件：CertificateSigningRequest.certSigningRequest 文件，点击Generate 

 ![image](/assets/20160921-2/14.png)


####6. 点击Download下载创建好的发布证书（cer后缀的文件），然后点击Done，你创建的发布证书就会存储在帐号中

 ![image](/assets/20160921-2/15.png)


####7. 双击安装。如果安装不上，可以直接将证书文件拖拽到钥匙串访问的列表中

###四、添加设备
####1、点击+添加设备到开发者账号中，为制作PP文件做准备

 ![image](/assets/20160921-2/16.png)

 ![image](/assets/20160921-2/17.png)


Name：设备的描述 可以随便填 方便你记忆

UDID：设备的标号

2、获取UUID(这里随便提供一种方法获取UUID)
将iPhone手机插入到电脑上 ，打开iTunes，然后按如图操作

 ![image](/assets/20160921-2/18.png)
 
 ![image](/assets/20160921-2/19.png)
 
 ![image](/assets/20160921-2/20.png)


3、填入UUID就OK了

###五、根据Devices创建Provisioning Profiles配置文件 （PP文件）
1、找到Provisioning Profiles ，点击All，然后点击右上角 + 号

 ![image](/assets/20160921-2/21.png)


2、 选择iOS App Developement，点击Continue

 ![image](/assets/20160921-2/22.png)


3、在App ID 这个选项栏里面找到你刚刚创建的：App IDs（Bundle ID） 类型的套装，点击Continue

 ![image](/assets/20160921-2/23.png)


4、选择你刚创建的发布证书（或者生成p12文件的那个发布证书），点击Continue

 ![image](/assets/20160921-2/241.png)

5、选择设备

 ![image](/assets/20160921-2/24.png)


>注意：wildCard格式的证书没有推送，PassCard等服务的应用，慎重选择。因为PP证书的开发者证书需要真机调试，所以我们需要绑定真机，这里因为之前添加过一些设备，所以这里就可以直接全选添加，如果没有的话，需要将真机的udid复制出来在此添加。在发布的PP文件中，是没有这一步的。

6、在Profile Name栏里输入一个名字（这个是PP文件的名字，可随便输入，在这里我用工程名字，便于分别），然后点击Generate

 ![image](/assets/20160921-2/25.png)


7、然后点击下载 ，将其下载下来

>双击就添加到Xcode中，这样在真机调试或者发布时，就可以分别有不同的PP证书与其对应。其实可以不用下载保存

---

###六、设置Xcode 真机调试
1、设置Bundle ID 和 申请的appid 一致

 ![image](/assets/20160921-2/26.png)


2、设置Debug的CER证书
3、配置证书描述文件(PP文件)

 ![image](/assets/20160921-2/27.png)


4、选择真机 进行真机调试

使用P12 文件 使多台Mac进行真机调试 (或者发布)【重点】
1、为什么要使用P12文件

当我们用大于三个mac设备开发应用时，想要申请新的证书，如果在我们的证书里，包含了3个发布证书，2个开发证书，可以发现再也申请不了开发证书和发布证书了（一般在我们的证书界面中应该只有一个开发证书，一个发布证书，没必要生成那么多的证书，证书一般在过期之后才会重新添加。）

 ![image](/assets/20160921-2/28.png)


这时候，再点击“+”时，就会发现点击不了开发和发布证书，也就是添加不了开发证书和发布证书了：

 ![image](/assets/20160921-2/29.png)

2、P12文件能解决什么问题
为了不能添加证书的问题我们有2个解决方案

第一种方法——“revoke”（不推荐）：

 ![image](/assets/20160921-2/30.png)


将以前的证书“revoke”掉，
然后重新生成一个新的证书。
这种方法是可以的，但是会造成相应的ProvisioningProfiles(PP文件)失效，这是小问题。但是又要重新申请证书甚至描述文件很浪费时间，所以不提倡这种做法。


第二种方法——“.p12”（推荐）：

我们的每一个证书都可以生成一个.p12文件，这个文件是一个加密的文件，只要知道其密码，就可以供给所有的mac设备使用，使设备不需要在苹果开发者网站重新申请开发和发布证书，就能使用。
3、P12文件是如何使用的

注意：一般.p12文件是给与别人使用的，本机必须已经有一个带秘钥的证书才可以生成.p12文件
导出一个带有私钥的证书(这里我选择调试证书 也就是调试的CER证书 ，其实也可以是 发布证书，只不过那就不用于调试 而是用于上架了）。然后点击导出

 ![image](/assets/20160921-2/31.png)


填好名字和储存位置，点击储存

 ![image](/assets/20160921-2/32.png)


填写该P12文件证书的密码，点“好”

 ![image](/assets/20160921-2/33.png)


然后生成P12文件

 ![image](/assets/20160921-2/35.png)


其实P12文件不仅是真机测试的时候用，上架的时候也会用，P12文件的使用方法，调试和上架是一样的。最简单的理解就是：把P12文件当做CER文件使用，调试就当调试CER，上架就当发布CER使用。
使用
调试：就是把该教程的第三步创建调试证书省略，将其换成P12文件即可
上架：把《iOS-最全的App上架教程》的第三步穿件发布证书省略，将其换成P12文件即可。

文／随梦而飞飞（简书作者）
原文链接：http://www.jianshu.com/p/c8e86f62687a
著作权归作者所有，转载请联系作者获得授权，并标注“简书作者”。

