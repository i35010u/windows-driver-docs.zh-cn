---
title: 文本日志部分标头的格式
description: 文本日志部分标头的格式
ms.assetid: ec46a540-e888-426d-85fc-6ad2d756c7b8
keywords:
- 部分标头 WDK SetupAPI 日志记录
- 格式 WDK SetupAPI 日志记录
- 文本日志 WDK SetupAPI，部分标头
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1802e4caf2a7998bc557004201e9756eb311a745
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377073"
---
# <a name="format-of-a-text-log-section-header"></a>文本日志部分标头的格式


一个*文本日志部分标头*包含两个日志条目。 第一个条目的格式包括"&gt; &gt; &gt; "前缀字符串，并按*section_title*字段和一个*instance_identifier*字段。 在以下示例中，斜体样式中的文本是部分创建者提供的特定部分的文本的占位符和粗体的字体样式的文本提供的 SetupAPI 日志记录。

```cpp
>>>  [section_title - instance_identifier] 
```

*Section_title*字段将始终存在，并为关联的部分与操作提供标题。

*Instance_identifier*提供的标识符，理想情况下，唯一标识该操作的实例。 如果*instance_identifier*字段不存在，部分标头的第一个条目的格式如下所示：

```cpp
>>>  [section_title] 
```

部分标头的第二个条目的格式包括"&gt; &gt; &gt; "前缀字符串，并按*time_stamp*字段和"部分启动"字符串，按如下所示：

```cpp
>>>  time_stamp Section start
```

格式*time_stamp*字段如下所示：

```cpp
yyyy/mm/dd hh:mm:ss.sss:
```

其中*time_stamp*子字段是按如下所示：

-   *yyyy*是 4 位数的年份， *mm*是两位数月份，和*dd*是 2 位数的日期

-   本地时间基于 24 小时制，其中*hh*为 2 位数字表示小时， *mm*是 2 位数表示分钟*ss* 2 位数字表示的秒数，并且 sss 的 3 位数字毫秒数。

下面是用户模式下插 (PnP) 管理器将创建的组安装操作的 PCI 设备的典型部分，标头的示例。 *Section_title*字段是"设备安装，" *instance_identifier*字段是设备实例标识符"PCI\\VEN_104C DEV_8019 SUBSYS_8010104C & REV_00\\3 61aaa01 & 0 38，"和*time_stamp*字段是"2005年/02/13 22:06:28.109:。"

```cpp
>>>  [Device Install - PCI\VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00\3&61aaa01&0&38]
>>>  2005/02/13 22:06:28.109: Section start
```

 

 





