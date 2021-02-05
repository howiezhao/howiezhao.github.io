---
title: Kali Rolling 2017 中无法登录 BeEF 的解决方案
date: 2018-02-08 19:18:51
categories: Bug
tags:
  - Kali
---

在 Kali Rolling 2017 中打开 BeEF 然后自动跳转到登录页面，会发现只有 BeEF 的图标而没有登录框，无法进行登录，经查是因为和 Metasploit 的集成有关的，解决方案如下：

将 `/usr/share/beef-xss/extensions/admin_ui/api/handler.rb` 文件中第 22 行的

```ruby
minified = Uglifier.compile(evaluated)
```

改为

```ruby
minified = evaluated
```

保存并重启 BeEF 即可。
