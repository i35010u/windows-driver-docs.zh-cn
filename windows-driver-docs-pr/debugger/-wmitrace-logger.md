---
title: wmitrace.logger
description: Wmitrace.logger 扩展显示有关跟踪会话，包括会话配置数据的数据。 此扩展不显示在会话期间生成的跟踪消息。
ms.assetid: 2bc456db-3e97-49f8-9c57-75ee5fee0f9d
keywords:
- wmitrace.logger Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.logger
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0e3224872752045ad29a6f0c57a70d638050cd40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327365"
---
# <a name="wmitracelogger"></a>!wmitrace.logger


**！ Wmitrace.logger**扩展显示有关跟踪会话，包括会话配置数据的数据。 此扩展不显示在会话期间生成的跟踪消息。

```dbgcmd
!wmitrace.logger [ LoggerID | LoggerName ]
```

## <a name="span-idddkwmittraceloggerdbgspanspan-idddkwmittraceloggerdbgspanparameters"></a><span id="ddk__wmittrace_logger_dbg"></span><span id="DDK__WMITTRACE_LOGGER_DBG"></span>参数


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
指定跟踪会话。 *LoggerID*是一个系统将分配到计算机上每个跟踪会话的序号。 如果未不指定任何参数，则使用跟踪会话 id 等于 1。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
指定跟踪会话。 *LoggerName*时的文本名称为指定开始跟踪会话时。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows 2000 和更高版本的 Windows 中可用。 如果你想要 Windows 2000 中使用此扩展，您必须先将复制 Wmitrace.dll 文件的 Windows 调试工具安装目录的 winxp 子目录到 w2kfre 子目录。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK。

<a name="remarks"></a>备注
-------

此扩展用于性能日志和事件，不能的人工可读的显示格式。 若要跟踪消息显示在跟踪会话缓冲区中，标头数据，以及使用[ **！ wmitrace.logdump**](-wmitrace-logdump.md)。

若要查找的跟踪会话的记录器 ID，请使用[ **！ wmitrace.strdump** ](-wmitrace-strdump.md)扩展。 或者，您可以使用 Tracelog 命令 tracelog-l 列出跟踪会话及其基本属性，包括记录器 id。

 

 





