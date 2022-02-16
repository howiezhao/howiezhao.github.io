---
title: Session、Cookie 和 Token
categories: CheatSheet
date: 2021-02-25 16:01:02
tags:
---

## Session

Session 是一种抽象的概念，它不止存在于 HTTP 中，在计算机的众多领域都有它的身影，比如在 SSH、tmux 中都有 Session 的出现。

Session 被直译为**会话**，顾名思义，它指客户端和服务器之间的连接会话。

## Cookie

Cookie 是一种具体的技术，它常被用在 HTTP 中，在其他领域很少见到 Cookie 的身影。

Cookie 可以理解为是 Session 这种概念的一种实现，通过 Cookie 可以确定客户端和服务器之间的连接会话，从而使无状态的 HTTP 协议有状态。

除 Cookie 之外，还可以使用带参数的 URL 来实现 Session 这种概念。

## Token

Token 直译为**令牌**，顾名思义，它常被用以客户端和服务器之间的身份认证。

Cookie 不仅可以用来实现上述的这种身份认证，也可以用来实现类似购物车这种场景。
