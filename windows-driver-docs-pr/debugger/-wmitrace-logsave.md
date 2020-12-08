---
title: wmitrace.logsave
description: Wmitrace. logsave 扩展将跟踪会话的跟踪缓冲区的当前内容写入文件。
keywords:
- wmitrace logsave Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.logsave
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d2a8eba1945a3bade22ab54c9dc435cd72d5c940
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823523"
---
# <a name="wmitracelogsave"></a>!wmitrace.logsave


**！ Wmitrace logsave** 扩展将跟踪会话的当前内容写入文件中。

```dbgcmd
!wmitrace.logsave {LoggerID|LoggerName} Filename 
```

## <a name="span-idddk__wmitrace_logsave_dbgspanspan-idddk__wmitrace_logsave_dbgspanparameters"></a><span id="ddk__wmitrace_logsave_dbg"></span><span id="DDK__WMITRACE_LOGSAVE_DBG"></span>参数


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span>*LoggerID*   
指定跟踪会话。 *LoggerID* 是系统分配给计算机上每个跟踪会话的序号。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span>*LoggerName*   
指定跟踪会话。 *LoggerName* 是启动跟踪会话时指定的文本名称。

<span id="_______Filename______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span>*Filename*   
为输出文件指定路径 (可选的) 和文件名。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展由 Wmitrace.dll 导出。

此扩展在 windows 2000 和更高版本的 Windows 中可用。 如果要将此扩展与 Windows 2000 一起使用，必须先将 Wmitrace.dll 文件从 Windows 的调试工具安装目录的 winxp 子目录复制到 w2kfre 子目录。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关事件跟踪的概念性概述，请参阅 Microsoft Windows SDK。 有关 Tracelog 的信息，请参阅 Windows 驱动程序工具包中的 "Tracelog" (WDK) 。

<a name="remarks"></a>备注
-------

此扩展只显示处于内存中的跟踪。 它不显示已从缓冲区刷新并传递到事件跟踪日志文件或跟踪使用者的跟踪消息。

跟踪会话缓冲区存储跟踪消息，直到它们被刷新到日志文件或跟踪使用者实时显示。 此扩展将物理内存中的缓冲区内容保存到指定文件中。

输出是以二进制格式编写的。 通常，这些文件使用 .etl (事件跟踪日志) 文件扩展名。

如果使用 Tracelog 启动具有循环缓冲的跟踪会话 ( 缓冲) ，则可以使用此扩展来保存当前缓冲区内容。

若要查找跟踪会话的记录器 ID，请使用 [**！ wmitrace**](-wmitrace-strdump.md) 扩展名。 另外，还可以使用 Tracelog 命令 Tracelog-l 来列出跟踪会话及其基本属性，其中包括记录器 ID。

 

 





