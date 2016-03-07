---
layout: post
title: "NSNumberFormatter的基本用法"
description: "NSNumberFormatter的基本用法"
category: iOS
tags: [学习]
---



#NSNumberFormatter的基本用法
```

  NSNumberFormatter *numberFormatter = [[NSNumberFormatteralloc] init];
    
    numberFormatter.locale = [[NSLocalealloc] initWithLocaleIdentifier:@"zh_CN"];//设置中文格式
    for (int i=0; i<6; i++)
    {
        [numberFormattersetNumberStyle:i];
        [numberFormattersetMinimumFractionDigits:2];
        [numberFormattersetMaximumFractionDigits:6];
        [numberFormatter setFormatterBehavior:NSNumberFormatterBehaviorDefault];
        NSString *formattedNumberString = [numberFormatterstringFromNumber:[NSNumbernumberWithDouble:123456.789]];
        
        NSLog(@"formattedNumberString :%d %@", i, formattedNumberString);
    }
    formatterNumberStyle对应的格式
    
    NSNumberFormatterNoStyle 123456.789
    NSNumberFormatterDecimalStyle  123,456.789
    NSNumberFormatterCurrencyStyle ￥123,456.789
    NSNumberFormatterPercentStyle  12,345,678.90%
    NSNumberFormatterScientificStyle 1.23457E5
    NSNumberFormatterSpellOutStyle 十二万三千四百五十六点七八九
    
    
    
    NSNumber *number = [NSNumbernumberWithLongLong:1234567890098765];
    NSNumberFormatter *formatter = [NSNumberFormatternew];
    [formatter setUsesGroupingSeparator:YES];设置用组分隔
    [formattersetGroupingSize:4];//四个一组
    [formatter setGroupingSeparator:@" "];组间用空格隔开
    NSString *string = [formatter stringFromNumber:number];
    string : 1234 5678 9009 8765
    //可以来设置银行卡号码

```