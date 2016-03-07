---
layout: post
title: "BASE64,MD5,SHA1"
description: "BASE64,MD5,SHA1"
category: iOS
tags: [学习]
---



#BASE64,MD5,SHA1
BASE64是一种常用的编码格式,严格来说不算是一种加密算法.常见于邮件、http加密.
iOS7.0后官方提供了编码解码的api GTMBase64也是经常用的编码解码的第三方库

```
@interface NSData (NSDataBase64Encoding)

/* Create an NSData from a Base-64 encoded NSString using the given options. By default, returns nil when the input is not recognized as valid Base-64.
*/
- (instancetype)initWithBase64EncodedString:(NSString *)base64String options:(NSDataBase64DecodingOptions)options NS_AVAILABLE(10_9, 7_0);

/* Create a Base-64 encoded NSString from the receiver's contents using the given options.
*/
- (NSString *)base64EncodedStringWithOptions:(NSDataBase64EncodingOptions)options NS_AVAILABLE(10_9, 7_0);

/* Create an NSData from a Base-64, UTF-8 encoded NSData. By default, returns nil when the input is not recognized as valid Base-64.
*/
- (instancetype)initWithBase64EncodedData:(NSData *)base64Data options:(NSDataBase64DecodingOptions)options NS_AVAILABLE(10_9, 7_0);

/* Create a Base-64, UTF-8 encoded NSData from the receiver's contents using the given options.
*/
- (NSData *)base64EncodedDataWithOptions:(NSDataBase64EncodingOptions)options NS_AVAILABLE(10_9, 7_0);

@end
```

MD5(信息摘要算法)是一种单向的,不可逆的Hash算法,一般用来做文件的校验,同一文件,生成的MD5值是唯一的,用两次取到的MD5来判断文件是否相同,

```
#import 
- (NSString *)stringMD5
{
    if(self == nil || [self length] == 0)
    {
        return nil;
    }
    
    const char *value = [self UTF8String];
    
    unsigned char outputBuffer[CC_MD5_DIGEST_LENGTH];
    CC_MD5(value, (CC_LONG)strlen(value), outputBuffer);
    
    NSMutableString *outputString = [[NSMutableString alloc] initWithCapacity:CC_MD5_DIGEST_LENGTH * 2];
    for(NSInteger count = 0; count < CC_MD5_DIGEST_LENGTH; count++){
        [outputString appendFormat:@"%02x",outputBuffer[count]];
    }
    
    return outputString;
}
```
SHA(安全散列算法)也是单向,不可逆的哈希算法,数字签名等密码学应用中重要的工具，被广泛地应用于电子商务等信息安全领域。和MD5差不多,但要比MD5安全一些,

```
+(NSString *)digest:(NSString *)input{
	NSData *data = [input dataUsingEncoding:NSASCIIStringEncoding allowLossyConversion:YES];
	uint8_t digest[CC_SHA1_DIGEST_LENGTH];
	CC_SHA1(data.bytes, (CC_LONG)data.length, digest);
	NSMutableString *output = [NSMutableString stringWithCapacity:CC_SHA1_DIGEST_LENGTH * 2];
	for (int i = 0; i < CC_SHA1_DIGEST_LENGTH; i++) {
		[output appendFormat:@"%02x",digest[i]];
	}
	return output;
}
```
研究的很浅,见谅!