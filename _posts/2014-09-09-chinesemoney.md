---
layout: post
title: "阿拉伯数字转换为大写金额"
description: "阿拉伯数字转换为大写金额"
category: iOS
tags: [学习]
---



#阿拉伯数字转换为大写金额


 遇到一个阿拉伯数字转换为大写金额的需求,看网上有的写的过于复杂,但是也有的写的特变简洁,自己写了一个仅供参考,如有问题,请及时指出,及时改正,谢谢!
 
 ```
/**
 *
 *  @param string 阿拉伯数字格式字符串
 *
 *  @return 返回一个大写金额
 */
-(NSString*)getCnMoneyByString:(NSString*)string{
    
    NSNumberFormatter *numberFormatter = [[NSNumberFormatter alloc] init];
    
    numberFormatter.locale = [[NSLocale alloc] initWithLocaleIdentifier:@"zh_CN"];
    
    [numberFormatter setNumberStyle:NSNumberFormatterSpellOutStyle];
    [numberFormatter setMinimumFractionDigits:2];
    [numberFormatter setMaximumFractionDigits:6];
    [numberFormatter setFormatterBehavior:NSNumberFormatterBehaviorDefault];
    NSString *formattedNumberString = [numberFormatter stringFromNumber:[NSNumber numberWithDouble:[string doubleValue]]];
    //通过NSNumberFormatter转换为大写的数字格式 eg:一千二百三十四
    
    //替换大写数字转为金额
    formattedNumberString = [formattedNumberString stringByReplacingOccurrencesOfString:@"一" withString:@"壹"];
    formattedNumberString = [formattedNumberString stringByReplacingOccurrencesOfString:@"二" withString:@"贰"];
    formattedNumberString = [formattedNumberString stringByReplacingOccurrencesOfString:@"三" withString:@"叁"];
    formattedNumberString = [formattedNumberString stringByReplacingOccurrencesOfString:@"四" withString:@"肆"];
    formattedNumberString = [formattedNumberString stringByReplacingOccurrencesOfString:@"五" withString:@"伍"];
    formattedNumberString = [formattedNumberString stringByReplacingOccurrencesOfString:@"六" withString:@"陆"];
    formattedNumberString = [formattedNumberString stringByReplacingOccurrencesOfString:@"七" withString:@"柒"];
    formattedNumberString = [formattedNumberString stringByReplacingOccurrencesOfString:@"八" withString:@"捌"];
    formattedNumberString = [formattedNumberString stringByReplacingOccurrencesOfString:@"九" withString:@"玖"];
    formattedNumberString = [formattedNumberString stringByReplacingOccurrencesOfString:@"〇" withString:@"零"];
    formattedNumberString = [formattedNumberString stringByReplacingOccurrencesOfString:@"千" withString:@"仟"];
    formattedNumberString = [formattedNumberString stringByReplacingOccurrencesOfString:@"百" withString:@"佰"];
    formattedNumberString = [formattedNumberString stringByReplacingOccurrencesOfString:@"十" withString:@"拾"];
    
    //对小数点后部分单独处理
    if ([formattedNumberString rangeOfString:@"点"].length>0) {
        
        NSArray* arr = [formattedNumberString componentsSeparatedByString:@"点"];
        
        NSMutableString* lastStr = [[arr lastObject] mutableCopy];
        
        if (lastStr.length>=2) {
            
            [lastStr insertString:@"分" atIndex:lastStr.length];
            
        }
        if (![[lastStr substringWithRange:NSMakeRange(0, 1)]isEqualToString:@"零"]) {
            [lastStr insertString:@"角" atIndex:1];
        }
        
        formattedNumberString = [[arr firstObject] stringByAppendingFormat:@"元%@",lastStr];
        
    }else{
        formattedNumberString = [formattedNumberString stringByAppendingString:@"元"];
    }
    
    return formattedNumberString;
    
}
```