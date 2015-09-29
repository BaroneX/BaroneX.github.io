---
layout: post
title: "Runtime消息转发机制"
description: "Runtime消息转发机制"
category: iOS
tags: [学习]
---


# 运行时消息转发机制
当你对一个对象发送消息,但是它无法响应次消息时,运行时会给你三次机会来试图挽救该消息.挽救失败-->就会爆出 'unrecognized selector sent to instance:XXXXX'这个常见的错误.


###第一次机会:运行时会给一次机会,让你提供方法来实现该消息,返回YES会继续进行提供的方法,返回NO就会进入第二次机会

	+ (BOOL)resolveInstanceMethod:(SEL)sel{
    return NO;
	}

###第二次机会:如果当前对象实现不了该方法,会让你提供一个可以实现该方法的对象,如果提供不了,那就进入最后一次机会

	- (id)forwardingTargetForSelector:(SEL)aSelector
	{
    return nil;
	}


###第三次机会:该方法提供了两个方式供你选择,1你可以换个对象执行当前方法,2换个方法执行

	-(void)forwardInvocation:(NSInvocation *)invocation{
    	
    	//1换个对象执行
    	[invocation invokeWithTarget:[ClassB new]];
    
    	//2换个方法执行
    	invocation.selector = @selector(methodB);
    	[invocation invokeWithTarget:self];
	}
	
以上是运行时消息转发机制.写的比较简单.
