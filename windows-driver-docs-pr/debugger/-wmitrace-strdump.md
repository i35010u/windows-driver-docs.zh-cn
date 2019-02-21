---
title: wmitrace.strdump
description: Wmitrace.strdump 扩展显示 WMI 事件跟踪结构。 您可以限制特定跟踪会话的结构的显示。
ms.assetid: 3fd1c4d5-c3c6-40b5-90f4-e5453bb56b19
keywords:
- wmitrace.strdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.strdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eed7fdf94c88568ab767bd8c2d4b72e8d7c0acd3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525372"
---
# <a name="wmitracestrdump"></a>!wmitrace.strdump


**！ Wmitrace.strdump**扩展显示 WMI 事件跟踪结构。 您可以限制特定跟踪会话的结构的显示。

```dbgcmd
!wmitrace.strdump [ LoggerID | LoggerName ] 
```

## <a name="span-idddkwmitracestrdumpdbgspanspan-idddkwmitracestrdumpdbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>参数


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
将显示限制为事件跟踪结构指定的跟踪会话。 *LoggerID*指定跟踪会话。 它是系统分配到计算机上每个跟踪会话的第几号。 如果未不指定任何参数，将显示所有跟踪会话。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
将显示限制为事件跟踪结构指定的跟踪会话。 *LoggerName*时的文本名称为指定开始跟踪会话时。 如果未不指定任何参数，将显示所有跟踪会话。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows 2000 和更高版本的 Windows 中可用。 如果你想要 Windows 2000 中使用此扩展，您必须先将复制 Wmitrace.dll 文件的 Windows 调试工具安装目录的 winxp 子目录到 w2kfre 子目录。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK。 有关跟踪日志的信息，请参阅"Tracelog"主题 Windows Driver Kit (WDK) 中。

<a name="remarks"></a>备注
-------

若要查找的跟踪会话的记录器 ID，请使用 **！ wmitrace.strdump**扩展。 或者，您可以使用 Tracelog 命令 tracelog-l 列出跟踪会话及其基本属性，包括记录器 id。

 

 





