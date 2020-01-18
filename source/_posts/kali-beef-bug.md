---
title: Kali Rolling 2017中无法登录BeEF的解决方案
date: 2018-02-08 19:18:51
categories: Bug
tags:
  - Kali
---

在Kali Rolling 2017中打开BeEF然后自动跳转到登录页面，会发现只有BeEF的图标而没有登录框，无法进行登录，经查是因为和Metasploit的集成有关的，解决方案如下：
将/usr/share/beef-xss/extensions/admin_ui/api/handler.rb文件中第22行的
```ruby
minified = Uglifier.compile(evaluated)
```
改为
```ruby
minified = evaluated
```
保存并重启BeEF即可。