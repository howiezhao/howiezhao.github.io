---
title: XML、JSON与YAML
date: 2018-07-21 19:50:23
categories: CheatSheet
tags:
---

XML、JSON与YAML是三种常见的信息标记形式，这三者由于其特有的属性而在不同的领域广为使用。
## XML
**XML**，Extensible Markup Language(可扩展标记语言)，倘若我要表示某个人的简要信息，用XML可写为：
```
<person>
    <firstName>Tian</firstName>
    <lastName>Song</lastName>
    <address>
        <streetAddr>中关村南大街5号</streetAddr>
        <city>北京市</city>
        <zipcode>100081</zipcode>
    </address>
    <prof>Computer System</prof><prof>Security</prof>
</person>
```

## JSON
**JSON**，JavaScript Object Notation(JavaScript对象表示法)，倘若我要表示某个人的简要信息，用JSON可写为：
```
{
    "firstName" : "Tian",
    "lastName" : "Song",
    "address" : {
                    "streetAddr" : "中关村南大街5号",
                    "city" : "北京市",
                    "zipcode" : "100081"
                },
    "prof" : ["Computer System", "Security"]
}
```

## YAML
**YAML**，在开发这种语言之初，其意为Yet Another Markup Language(仍是一种标记语言)，之后为了强调这种语言以数据作为中心，而不是以标记语言为重点，故解释为YAML Ain't a Markup Language(YAML不是一种标记语言)，倘若我要表示某个人的简要信息，用YAML可写为：
```
firstName : Tian
lastName : Song
address : 
    streetAddr : 中关村南大街5号
    city : 北京市
    zipcode : 100081
prof : 
-Computer System
-Security
```

## 比较
XML是最早的通用信息标记语言，可扩展性好，但繁琐，主要用于Internet上的信息交互与传递，以及用户界面的编写，比如Android；JSON中的信息有类型，适合程序处理(js)，较XML简洁，主要用于移动应用云端和节点的信息通信，无注释；YAML信息无类型，文本信息比例最高，可读性好，主要用于各类系统的配置文件，有注释易读。