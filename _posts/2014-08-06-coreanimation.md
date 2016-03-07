---
layout: post
title: "CoreAnimation的基本用法"
description: "CoreAnimation的基本用法"
category: iOS
tags: [学习]
---



#CoreAnimation的基本用法
```
@interface ViewController ()
{    
    CustomButton* but;
    int currentCount;
}
@end

@implementation ViewController

- (void)viewDidLoad
{
    [super viewDidLoad];
    
    but = [[CustomButton alloc]initWithFrame:CGRectMake(0,0, 64, 64)];//接上一篇重绘的按钮

    [self.view addSubview:but];
    [but addTarget:self action:@selector(click) forControlEvents:UIControlEventTouchUpInside];
    
	// Do any additional setup after loading the view, typically from a nib.
}
-(void)click{

    switch (currentCount%4) {
        case 0:
        {
            CABasicAnimation* anim = [CABasicAnimation animationWithKeyPath:@"position"];
            anim.fromValue = [NSValue valueWithCGPoint:CGPointMake(0, 0)];
            anim.toValue = [NSValue valueWithCGPoint:CGPointMake(160, 288)];
            anim.duration = 2;
            but.layer.position = CGPointMake(160, 288);
            anim.removedOnCompletion = YES;
            [but.layer addAnimation:anim forKey:nil];
        }
            break;
        case 1:{
            
            CABasicAnimation* anim = [CABasicAnimation animationWithKeyPath:@"transform"];
            CATransform3D fromValue = but.layer.transform;
            // 设置动画开始的属性值
            anim.fromValue = [NSValue valueWithCATransform3D:fromValue];
            // 绕X轴旋转180度
            CATransform3D toValue = CATransform3DRotate(fromValue, M_PI , 1 , 0 , 0);
            // 绕Y轴旋转180度
            //	CATransform3D toValue = CATransform3DRotate(fromValue, M_PI , 0 , 1 , 0);
            //	// 绕Z轴旋转180度
            //	CATransform3D toValue = CATransform3DRotate(fromValue, M_PI , 0 , 0 , 1);
            // 设置动画结束的属性值
            anim.toValue = [NSValue valueWithCATransform3D:toValue];
            anim.duration = 0.5;
            anim.repeatCount = 13;
            but.layer.transform = toValue;
            anim.removedOnCompletion = YES;
            // 为imageLayer添加动画
            [but.layer addAnimation:anim forKey:nil];
        }break;
        case 2:{
            CAKeyframeAnimation* anim = [CAKeyframeAnimation
                                         animationWithKeyPath:@"transform"];
            // 设置CAKeyframeAnimation控制transform属性依次经过的属性值
            anim.values = [NSArray arrayWithObjects:
                           [NSValue valueWithCATransform3D:but.layer.transform],
                           [NSValue valueWithCATransform3D:CATransform3DScale
                            (but.layer.transform , 0.2, 0.2, 1)],
                           [NSValue valueWithCATransform3D:CATransform3DScale
                            (but.layer.transform, 2, 2 , 1)],
                           [NSValue valueWithCATransform3D:but.layer.transform], nil];
            anim.duration = 5;
            anim.removedOnCompletion = YES;
            // 为imageLayer添加动画
            [but.layer addAnimation:anim forKey:nil];
            
        }
            break;
        case 3:{
            
            CABasicAnimation* anim = [CABasicAnimation animationWithKeyPath:@"transform"];
            CATransform3D fromTransValue = but.layer.transform;
            // 设置动画开始的属性值
            anim.fromValue = [NSValue valueWithCATransform3D:fromTransValue];
            // 绕X轴旋转180度
            CATransform3D toTransValue = CATransform3DRotate(fromTransValue, M_PI , 1 , 0 , 0);
            // 绕Y轴旋转180度
            //	CATransform3D toValue = CATransform3DRotate(fromValue, M_PI , 0 , 1 , 0);
            //	// 绕Z轴旋转180度
            //	CATransform3D toValue = CATransform3DRotate(fromValue, M_PI , 0 , 0 , 1);
            // 设置动画结束的属性值
            anim.toValue = [NSValue valueWithCATransform3D:toTransValue];
            anim.duration = 0.5;
            anim.repeatCount = 13;
            but.layer.transform = toTransValue;
            anim.removedOnCompletion = YES;
            // 为imageLayer添加动画
            [but.layer addAnimation:anim forKey:nil];
            anim.removedOnCompletion = YES;
            // 创建不断改变CALayer的transform属性的属性动画
            CABasicAnimation* transformAnim = [CABasicAnimation
                                               animationWithKeyPath:@"transform"];
            CATransform3D fromValue = but.layer.transform;
            // 设置动画开始的属性值
            transformAnim.fromValue = [NSValue valueWithCATransform3D: fromValue];
            // 创建缩放为X、Y两个方向上缩放为0.5的变换矩阵
            CATransform3D scaleValue = CATransform3DScale(fromValue , 0.5 , 0.5, 1);
            // 绕Z轴旋转180度的变换矩阵
            CATransform3D rotateValue = CATransform3DRotate(fromValue, M_PI , 0 , 0 , 1);
            // 计算两个变换矩阵的和
            CATransform3D toValue = CATransform3DConcat(scaleValue, rotateValue);
            // 设置动画技术的属性值
            transformAnim.toValue = [NSValue valueWithCATransform3D:toValue];
            // 动画效果累加
            transformAnim.cumulative = YES;
            // 动画重复执行2次，旋转360度
            transformAnim.repeatCount = 2;
            transformAnim.duration = 3;
            // 位移、缩放、旋转组合起来执行
            CAAnimationGroup *animGroup = [CAAnimationGroup animation];
            animGroup.animations = [NSArray arrayWithObjects:anim
                                    , transformAnim , nil];
            animGroup.duration = 6;
            // 为imageLayer添加动画
            [but.layer addAnimation:animGroup forKey:nil];
            
            
        }
        default:
            break;
    }
    currentCount++;
}
```