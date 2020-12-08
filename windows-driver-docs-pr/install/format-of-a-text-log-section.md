---
title: 文本日志部分的格式
description: 文本日志部分的格式
keywords:
- 节 WDK Setupapi.log 日志记录
- 格式化 WDK Setupapi.log 日志记录
- 文本日志 WDK Setupapi.log，章节
- Setupapi.log 日志记录 WDK Windows Vista，文本日志部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57d18b8b32d0138d2b5f3f422727277db799a14f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820159"
---
# <a name="format-of-a-text-log-section"></a>文本日志部分的格式


*文本日志节* 包含一个节标头，该标头可打开部分，其中包含一系列应用于该节操作的日志条目，以及关闭该部分的节页脚。 节项在节中的显示顺序与它们写入部分的顺序相同。

以下文本日志部分的示例显示了典型部分的常规格式，其中斜体字体样式中的字段是特定于节的文本的占位符，而其余文本以粗体字体样式是 Setupapi.log 提供的通用文本。 前两个日志项构成了节标头，最后两个日志项构成了节页脚。

```cpp
>>>  [section_title - instance_identifier]
>>> time_stamp Section start
 section body log entry
 section body log entry
 section body log entry
<<<  [time_stamp: Section end]
<<<  [Exit Status(status_value)]
```

记录的节正文项取决于为日志设置的事件级别以及为日志启用的类别级别。 有关这些设置的详细信息，请参阅 [Setupapi.log 日志记录注册表设置](setupapi-logging-registry-settings.md)。

下面是文本日志部分的典型示例，即插即用 (PnP) 管理器创建的日志记录因 PCI 设备安装的条目。 在节标头中，" *section_title* " 字段为 "设备安装"， *instance_identifier* 字段为设备实例标识符 "PCI VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00 \\ \\ 3&61aaa01&0&38"，" *time_stamp* " 字段为 "2005/02/13 22：06：28.109："。 在节页脚中，" *status_value* " 字段为 "0x00000000"， *time_stamp* 字段为 "2005/02/13 22：06：20.000："。 此示例仅包括前三个部分的正文日志条目。 此示例的事件级别已设置为 TXTLOG_DETAILS 并为此示例启用了所有类别级别。

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

有关文本日志部分的内容和格式的详细信息，请参阅 [文本日志节标头的格式](format-of-a-text-log-section-header.md)、 [文本日志节正文](format-of-a-text-log-section-body.md)的格式和 [文本日志节脚注的格式](format-of-a-text-log-section-footer.md)。

 

 





