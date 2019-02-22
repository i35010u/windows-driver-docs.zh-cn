---
title: wmitrace.eventlogdump
description: Wmitrace.eventlogdump 扩展显示指定记录器的内容。 显示的格式与事件日志。
ms.assetid: 27254b36-b413-45f0-9834-ff55fbb787c7
keywords:
- wmitrace.eventlogdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.eventlogdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 401564686ba5d3c6e2447ebe3bbd222a32a2fc59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554145"
---
# <a name="wmitraceeventlogdump"></a>!wmitrace.eventlogdump


**！ Wmitrace.eventlogdump**扩展将显示指定记录器的内容。 显示的格式与事件日志。

```dbgcmd
!wmitrace.eventlogdump { LoggerID | LoggerName }
```

## <a name="span-idddkwmitracestrdumpdbgspanspan-idddkwmitracestrdumpdbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>参数


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
指定跟踪会话。 *LoggerID*是一个系统将分配到计算机上每个跟踪会话的序号。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
指定跟踪会话。 *LoggerName*时的文本名称为指定开始跟踪会话时。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows 2000 和更高版本的 Windows 中可用。 如果你想要 Windows 2000 中使用此扩展，您必须先将复制 Wmitrace.dll 文件的 Windows 调试工具安装目录的 winxp 子目录到 w2kfre 子目录。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK。 有关跟踪工具的信息，请参阅 Windows Driver Kit (WDK)。

<a name="remarks"></a>备注
-------

此扩展是类似于[ **！ wmitrace.logdump** ](-wmitrace-logdump.md)扩展，不同之处在于的输出 **！ wmitrace.eventlogdump**事件日志样式，和的输出格式 **！ wmitrace.logdump**格式化为 Windows 软件跟踪预处理器 (WPP) 样式。 应选择其格式适合于你想要显示的数据的扩展。

若要查找的跟踪会话的记录器 ID，请使用[ **！ wmitrace.strdump** ](-wmitrace-strdump.md)扩展。 或者，您可以使用 Tracelog 命令 tracelog-l 列出跟踪会话及其基本属性，包括记录器 id。

 

 





