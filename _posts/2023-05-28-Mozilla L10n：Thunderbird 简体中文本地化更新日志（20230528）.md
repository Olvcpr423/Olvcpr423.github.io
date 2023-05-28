---
layout: post
title: 'Mozilla L10n：Thunderbird 简体中文本地化更新日志（20230528）'
subtitle: '此更改预计在 115 版本向正式版渠道用户提供'
date: 2023-05-28
categories: 翻译
cvr: '/assets/img/hero.jpg'
tags: 翻译 Mozilla
---

**\>\>\> 20230528 更新日志 \<\<\<**

此前，Thunderbird 设置界面部分选项字符串的译文以冒号结尾，access key 则由程序自动添加在字符串的最末尾，恰好是在冒号的后方（如“每次显示：(O)  %S小时”）。这样既不美观，也可能引起歧义。因此，我们选择在不影响语义的前提下，将相关字符串的冒号全部移除，更改过后预期显示效果举例为“每次显示(O)  %S小时”，参见下图。

![更改前后的对比图。左图中部分 access key 出现在冒号后方，右图中将这些字符串的冒号去除](/assets/img/Mozilla L10n：Thunderbird 简体中文本地化更新日志（20230528）/compare.png "对比图：左为更改前，右为更改后")

祝使用愉快！

**\>\>\> 20230528 工作笔记 \<\<\<**

按照[微软的简体中文本地化标准](https://www.microsoft.com/zh-cn/language/StyleGuides)，access key 不应出现在标点符号后方。（所以原则上按钮文本诸如“浏览…(B)”也应改成“浏览(B)…”。）理想的做法是使用 `&` 方法手动将 access key 放到标点符号前（示例：`每次显示(&O)：  %S小时`)，但很遗憾 Mozilla 软件的大部分字符串使用 [Fluent 语法](https://mozilla-l10n.github.io/localizer-documentation/tools/fluent/basic_syntax.html)，需要在 FTL 中的 `.accesskey` 片段中指定 access key，如

```
visible-hours-label =
    .value = 每次显示
    .accesskey = o
```

，而不支持 `&`+`<access key>` 的操作。于是我想出一个“曲线救国”的办法（虽然出于跨平台兼容性问题最终无法采用。如果你所本地化的软件不受跨平台兼容性限制，可酌情参考此做法，详见下文）。

大家知道，access key 的标注规则是：

* 如果字符串中无与 access key 相同的字符，则程序会用半角空格括注 access key，不带空格地加在字符串末尾（如上文所举的例子）；

* 如果字符串中含相同的字符，那么程序就会直接在相应字符下方标注下划线，指示此字符为 access key（如字符串 `接受第三方 Cookie`，access key 为 `C`，那么显示样式就会是“接受第三方 <u>C</u>ookie”）。

基于此原理，我们可以骚操作一波：直接在字符串中按格式包含一个 access key：

```
visible-hours-label =
    .value = 每次显示(O)：
    .accesskey = o
```
如此一来，由于字符串中含与 access key 相同的字符，显示效果就将会是“每次显示(<u>O</u>)：”，这原是极好的。但很可惜，Thunderbird 是一个运行在 Windows、macOS 与 Linux 上的跨平台软件，上面这个方案并不兼容所有这些系统，如 macOS 就没有 access key 而只有 shortcut key<sup>[1]</sup>，因此 access key 在 macOS 上会隐藏，而上面这个方案会导致 access key 在所有平台上都显示出来，误导用户操作。因此最终没有采用这个方案，只好妥协将冒号去掉。

省略号的问题就只能忍忍了，删除省略号会影响语义（省略号代表点击按钮后仍需进一步操作），因此不能去掉。

---

注释：access key、shortcut key 及相关术语的定义，参见[微软文风指南上的说明](https://learn.microsoft.com/en-us/style-guide/a-z-word-list-term-collections/term-collections/keys-keyboard-shortcuts)。
