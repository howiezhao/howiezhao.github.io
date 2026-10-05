---
title: iCalendar 是什么
categories: CheatSheet
date: 2026-10-03 11:00:00
tags:
---

iCalendar 是通用的日历数据交换标准，常用于在多个不同日历系统之间分享日程，其后缀名常为 `.ics`。

一个典型的 iCalendar 文件内容如下所示：

```text
BEGIN:VCALENDAR
VERSION:2.0
PRODID:-//howiezhao//ical-demo//CN
NAME:iCal Demo
BEGIN:VEVENT
UID:uid1@howiezhao.com
DTSTAMP:20261003T110000Z
DTSTART:20261010T170000Z
DTEND:20261011T035959Z
SUMMARY:Coding Party
END:VEVENT
END:VCALENDAR
```

iCalendar 文件的第一行必须是 `BEGIN:VCALENDER`，最后一行必须是 `END:VCALENDER`；两行之间数据称之为“icalbody”。icalbody 由一系列**日历属性**和一个以上的**日历组件**组成。

<!-- more -->

日历属性被应用于整个日历，常见的字段有：

- `VERSION`：iCalendar 格式版本
- `PRODID`：即 Product Identifier，产品标识符。用来标识“这个 ICS 文件是由谁/什么程序生成的”。通常格式类似：`-//组织或域名//产品名称//语言`
- `NAME`：标准的日历名称属性
- `DESCRIPTION`：标准的日历描述属性

除此之外，也可以包含一些以 `X-` 开头的非标准扩展属性（X-property）：

- `X-WR-CALNAME`：常见的日历显示名称扩展
- `X-WR-CALDESC`：常见的日历描述扩展
- `X-WR-TIMEZONE`：日历默认时区

日历组件有很多类型，常见的类型为 **VEVENT**（事件）和 **VTODO**（待办事项）。我们重点介绍 VEVENT 的格式。

一个 VEVENT 类型的日历组件通过 `BEGIN:VEVENT` 与 `END:VEVENT` 包裹，其中的字段含义如下：

- `UID`：即 Unique Identifier，事件的唯一标识符
- `DTSTAMP`：事件对象被创建/生成时的时间
- `DTSTART`：事件的开始时间
- `DTEND`：事件的结束时间
- `SUMMARY`：事件的标题
- `DESCRIPTION`：事件的详细描述
- `TRANSP`：即 Time Transparency，它控制这个事件是否会占用日历的忙闲时间（Free/Busy）。值 `TRANSPARENT` 表示这个事件不会把这段时间标记成“忙”。反正，值 `OPAQUE` 表示这个事件会占用这段时间，通常视为 Busy。
- `LOCATION`：事件地点
- `GEO`：事件地点的地理坐标，格式为`纬度;经度`
- `RRULE`：即 Recurrence Rule，重复规则。以 `RRULE:FREQ=YEARLY;INTERVAL=1;BYMONTH=2;BYMONTHDAY=12` 为例，其表示每年重复一次，在每年的 2 月 12 日。

GitHub 上的[中国节假日补班日历](https://github.com/lanceliao/china-holiday-calender)项目提供了每年的调休 iCalendar 文件。导入Google Calendar后，即可显示调休情况。

[农历周期活动](https://howiezhao.github.io/lunar-events/)项目可以生成每年重复的农历周期活动，并导出为 ICS 文件。
