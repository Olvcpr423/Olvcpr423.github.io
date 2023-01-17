---
layout: post
title: 'Mozilla L10n：关于更改对 Safari 一词的翻译策略的提示'
subtitle: 'Notice of the change in the translate policy for the word Safari'
date: 2023-01-17
categories: Mozilla L10n
cvr: '/assets/img/hero.jpg'
tags: Mozilla 翻译
---

鉴于 Apple 自 iOS 11/macOS High Sierra 开始已将系统内置的网络浏览器名称（简体中文）由“Safari”更改为“Safari 浏览器”，为了与系统保持一致，提升用户体验一致性，经综合考虑，现对 Safari 一词的翻译策略做一些调整，细则如下：

***

1. 将 Firefox、Firefox for iOS、Focus for iOS 等在 Apple 操作系统上提供的软件，以及其他项目中仅适用于 Apple 操作系统的字符串（例如 [Common Voice 项目中这条仅适用于 iOS 的报错信息](https://pontoon.mozilla.org/zh-CN/all-projects/all-resources/?string=209891)）中的“Safari”翻译为“Safari 浏览器”。依实际情况，其应通过下列方式之一来实现：

    **情况 1**<br>原文：`{ -brand-name-safari }`<br>译文：`{ -brand-name-safari } 浏览器`

    **情况 2**<br>原文：`Safari`<br>译文：`Safari 浏览器`

**【注意】** 特别地，[此字符串](https://pontoon.mozilla.org/zh-CN/all-projects/all-resources/?string=210576) 属于 term，其译文将被应用到 `{ -brand-name-safari }` 所处的位置，所以不能被翻译成“Safari 浏览器”。

2. 对于其他项目中并非仅适用于Apple操作系统的字符串中的“Safari”，则依旧不翻译（例如 [这个面向所有用户提供的“浏览器对比”页面](https://www.mozilla.org/zh-CN/firefox/browsers/compare/safari/)）

此后的翻译应该延续这些规则，以保持一致性。如对此次更改有疑问或意见，请电邮至 oliverchan86[at]outlook.com 提出。祝贡献愉快！

***

简体中文审阅员（Translator）<br>**Olvcpr423**（Not affiliated with Mozilla）
