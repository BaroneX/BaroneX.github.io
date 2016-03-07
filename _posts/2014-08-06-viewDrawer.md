---
layout: post
title: "iOS UIView及其子类的重绘"
description: "iOS UIView及其子类的重绘"
category: iOS
tags: [学习]
---



#iOS UIView及其子类的重绘



开发自定义的UIView及其子类,有时候会比较多的用到drawRect方法,这个方法是一个重写
类型的方法,不重写的话,默认是执行父类的drawRect方法,和重绘有关的API都是CoreGraphics库里的API,刚开始使用时候,感觉和传统的objective-c风格的API有较大差异,但是熟悉之后就会好很多,很多方法 根据意思就能看明白,这是比较方便的.


	绘图的关键步骤,
	1.获取视图的上下文信息,就是获取一块画画的画布,
	2.使用CoreGraphics风格的API或者objective-c风格的API进行绘制

```
//获取画布
CGContextRef ctx =UIGraphicsGetCurrentContext();
{
// 开始定义路径
CGContextBeginPath(ctx);
// 添加一段圆弧，最后一个参数1代表逆时针，0代表顺时针
CGContextAddArc(<#CGContextRef c#>画布, <#CGFloat x#>原点x坐标, <#CGFloat y#>原点y坐标, <#CGFloat radius#>半径, <#CGFloat startAngle#>开始的弧度, <#CGFloat endAngle#>结束的弧度, <#int clockwise#>)
//关闭路径
CGContextClosePath(ctx);
// 设置填充颜色
CGContextSetRGBFillColor(<#CGContextRef context#>画布, <#CGFloat red#>, <#CGFloat green#>, <#CGFloat blue#>, <#CGFloat alpha#>)
// 填充当前路径。
CGContextFillPath(ctx);
// 关闭路径
CGContextClosePath(ctx);
//保存状态
}
CGContextSaveGState(ctx);
```
```
大括号之间的代码可以换成OC风格的代码
{
//// Color Declarations
UIColor* fillColor = [UIColor colorWithRed: 1 green: 1 blue: 1 alpha: 1];
UIColor* strokeColor = [UIColor colorWithRed: 0 green: 0 blue: 0 alpha: 1];

//// Oval Drawing
UIBezierPath* ovalPath = [UIBezierPath bezierPathWithOvalInRect: CGRectMake(81.5, 30.5, 49, 47)];
[fillColor setFill];
[ovalPath fill];
[strokeColor setStroke];
ovalPath.lineWidth = 1;
[ovalPath stroke];
}
两种代码都差不多,个人比较喜欢OC风格的
```
UIview及其子类都有一个setNeedsDisplay的方法,调用这个方法,会调用drawRect方法再次重绘

例子:

```
#import "CustomButton.h"

@implementation CustomButton

-(void)drawRect:(CGRect)rect{
    
    
    
    CGContextRef ctx = UIGraphicsGetCurrentContext();
    
    for (int i = 0; i<10; i++) {
        UIBezierPath* path = [UIBezierPath bezierPath];
        NSLog(@"%f",(self.frame.origin.y+self.frame.size.width/2));
        [path addArcWithCenter:CGPointMake(self.frame.size.width/2,self.frame.size.height/2) radius:(self.frame.size.width-i*40) startAngle:0 endAngle:M_PI*2 clockwise:0];
        UIColor* fillColor;
        if (i%2) {
            
            fillColor = [UIColor colorWithRed: 0 green: 0 blue: 0 alpha: 1];
        }else{
            
            fillColor = [UIColor colorWithRed: 1 green: 0 blue: 0 alpha: 1];
        }
        [fillColor setFill];
        [path fill];
    }


    CGContextSaveGState(ctx);
}
@end
```
```
在主界面添加自定义的按钮
    CustomButton* but = [[CustomButton alloc]initWithFrame:CGRectMake(0,100 , 320, 320)];

    [self.view addSubview:but];
    [but addTarget:self action:@selector(click) forControlEvents:UIControlEventTouchUpInside];
下面的就是重绘的按钮,有点大了,
```
 ![image](/assets/images/20140806.png)

绘图是一件有意思的事情,你可以自己发挥想象力,绘出许多有意思的东西,最后推荐一款软件PaintCode,看名字大概就知道什么意思了,是个BUG啊.
Enjoy yourself;
