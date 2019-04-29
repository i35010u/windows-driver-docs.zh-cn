---
title: 文本日志部分的格式
description: 文本日志部分的格式
ms.assetid: e0f7227c-6cd8-4c66-a38b-104f222847bc
keywords:
- 部分 WDK SetupAPI 日志记录
- 格式 WDK SetupAPI 日志记录
- 文本日志 WDK SetupAPI，部分
- SetupAPI 日志记录 WDK Windows Vista 中，文本日志部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5de5987659e98dcc817d89d99a4eca1d9cff770f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377063"
---
# <a name="format-of-a-text-log-section"></a>文本日志部分的格式


一个*文本日志部分*包括将打开部分中的部分标头，包括日志条目适用于部分操作，和关闭部分中的部分页脚的一系列节正文。 部分编写的相同顺序的部分中显示部分项。

文本日志部分的下面的示例演示一个典型的部分中，其中倾斜字体样式中的字段都是特定于部分的文本的占位符，粗体的字体样式中的剩余文本是由安装程序 Api 提供的通用文本的一般格式。 第一个的两个日志条目包含部分标头，最后两个日志条目包含部分页脚。

```cpp
>>>  [section_title - instance_identifer]
>>> time_stamp Section start
 section body log entry
 section body log entry
 section body log entry
<<<  [time_stamp: Section end]
<<<  [Exit Status(status_value)]
```

记录的部分正文条目取决于为日志设置的事件级别和启用的日志类别级别。 有关这些设置的详细信息，请参阅[SetupAPI 日志记录注册表设置](setupapi-logging-registry-settings.md)。

下面是插即用 (PnP) 管理器创建日志条目相关的 PCI 设备安装到的文本日志部分的典型示例。 在部分标题中， *section_title*字段是"设备安装，" *instance_identifier*字段是设备实例标识符"PCI\\VEN_104C DEV_8019 & SUBSYS_8010104 & REV_00\\3 61aaa01 & 0 38，"和*time_stamp*字段是"2005年/02/13 22:06:28.109:。" 在部分页脚*status_value*字段是"0x00000000"和*time_stamp*字段是"2005年/02/13 22:06:20.000:。" 在此示例中包含仅的第三个部分正文日志条目。 此示例中的事件级别已设置为 TXTLOG_DETAILS 并且已为此示例启用所有类别级别。

```cpp
>>>  [Device Install - PCI\VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00\3&61aaa01&0&38]
>>>  2005/02/13 22:06:20.000: Section start
     ndv: Retrieving device info...
     ndv: Setting device parameters...
     ndv: Building driver list...
...  
...  additional section body log entries, which are not shown
...  
<<<  [2005/02/13 22:06:28.109: Section end]
<<<  [Exit Status(0x00000000)]
```

有关内容和格式的文本日志部分的详细信息，请参阅[文本日志部分标头的格式](format-of-a-text-log-section-header.md)，[格式的文本日志部分正文](format-of-a-text-log-section-body.md)，和[文本日志部分的格式页脚](format-of-a-text-log-section-footer.md)。

 

 





