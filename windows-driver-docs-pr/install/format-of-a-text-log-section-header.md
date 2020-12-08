---
title: 文本日志部分标头的格式
description: 文本日志部分标头的格式
keywords:
- 节标头 WDK Setupapi.log 日志记录
- 格式化 WDK Setupapi.log 日志记录
- 文本日志 WDK Setupapi.log，节标头
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28bd20d61b5058f381e582796f3c9aef103ffa6c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820171"
---
# <a name="format-of-a-text-log-section-header"></a>文本日志部分标头的格式


*文本日志节标头* 包括两个日志条目。 第一项的格式包括 " &gt; &gt; &gt; " 前缀字符串，后跟一个 *section_title* 字段和一个 *instance_identifier* 字段。 在下面的示例中，以斜体字体样式显示的文本是节特定文本的占位符，由部分创建者提供，粗体字体样式的文本由 Setupapi.log 日志记录提供。

```cpp
>>>  [section_title - instance_identifier] 
```

*Section_title* 字段始终存在，并为与部分关联的操作提供标题。

*Instance_identifier* 提供一个标识符，该标识符在理想情况下唯一标识操作的实例。 如果 " *instance_identifier* " 字段不存在，则节标头的第一项的格式如下所示：

```cpp
>>>  [section_title] 
```

节标头的第二个条目的格式包括 " &gt; &gt; &gt; " 前缀字符串，后跟一个 *time_stamp* 字段和一个 "节开始" 字符串，如下所示：

```cpp
>>>  time_stamp Section start
```

*Time_stamp* 字段的格式如下所示：

```cpp
yyyy/mm/dd hh:mm:ss.sss:
```

其中 *time_stamp* 子字段如下所示：

-   *yyyy* 是4位数的年份， *mm* 是2位数的月份，而 *dd* 是两位数的日期

-   本地时间基于24小时制，其中， *hh* 是2位数的小时， *mm* 是2位数字的分钟， *ss* 是2位数的秒数，sss 是3位数的毫秒数。

下面是典型的节标头的示例，用户模式即插即用 (PnP) manager 将创建该标头以对 PCI 设备的安装操作进行分组。 " *Section_title* " 字段为 "设备安装"， *instance_identifier* 字段是设备实例标识符 "PCI \\ VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00 \\ 3&61aaa01&0&38"，" *time_stamp* " 字段为 "2005/02/13 22：06：28.109："。

```cpp
>>>  [Device Install - PCI\VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00\3&61aaa01&0&38]
>>>  2005/02/13 22:06:28.109: Section start
```

 

 





