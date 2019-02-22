---
title: wmitrace.logsave
description: Wmitrace.logsave 扩展将写入文件跟踪会话的跟踪缓冲区的当前内容。
ms.assetid: 713fea09-d405-4142-b2e8-29c813a4c3b6
keywords:
- wmitrace.logsave Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.logsave
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 161bd2db2b65095be689769cfa5e2733024b2653
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543233"
---
# <a name="wmitracelogsave"></a>!wmitrace.logsave


**！ Wmitrace.logsave**扩展将跟踪会话跟踪缓冲区的当前内容写入文件。

```dbgcmd
!wmitrace.logsave {LoggerID|LoggerName} Filename 
```

## <a name="span-idddkwmitracelogsavedbgspanspan-idddkwmitracelogsavedbgspanparameters"></a><span id="ddk__wmitrace_logsave_dbg"></span><span id="DDK__WMITRACE_LOGSAVE_DBG"></span>参数


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
指定跟踪会话。 *LoggerID*是一个系统将分配到计算机上每个跟踪会话的序号。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
指定跟踪会话。 *LoggerName*时的文本名称为指定开始跟踪会话时。

<span id="_______Filename______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *文件名*   
指定的路径 （可选） 和输出文件的文件名。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows 2000 和更高版本的 Windows 中可用。 如果你想要 Windows 2000 中使用此扩展，您必须先将复制 Wmitrace.dll 文件的 Windows 调试工具安装目录的 winxp 子目录到 w2kfre 子目录。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK。 有关跟踪日志的信息，请参阅"Tracelog"Windows Driver Kit (WDK) 中。

<a name="remarks"></a>备注
-------

此扩展显示时将内存中的跟踪。 它不会显示已从缓冲区刷新并传递到事件跟踪日志文件或跟踪使用者跟踪消息。

跟踪会话缓冲区存储跟踪消息，直到它们被刷新到日志文件或实时显示的跟踪使用者。 此扩展将保存到指定的文件的物理内存中缓冲区的内容。

以二进制格式写入输出。 通常情况下，这些文件使用.etl （事件跟踪日志） 文件扩展名。

当您使用 Tracelog 循环缓冲启动跟踪会话 (-缓冲)，可以使用此扩展来保存当前缓冲区的内容。

若要查找的跟踪会话的记录器 ID，请使用[ **！ wmitrace.strdump** ](-wmitrace-strdump.md)扩展。 或者，您可以使用 Tracelog 命令 tracelog-l 列出跟踪会话及其基本属性，包括记录器 id。

 

 





