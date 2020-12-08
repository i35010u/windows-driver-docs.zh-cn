---
title: wmitrace.strdump
description: Wmitrace. strdump 扩展显示 WMI 事件跟踪结构。 您可以将显示范围限制为特定跟踪会话的结构。
keywords:
- wmitrace strdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.strdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b0070955a3a28aee906de376654eae381969ff5d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819361"
---
# <a name="wmitracestrdump"></a>!wmitrace.strdump


**！ Wmitrace strdump** 扩展显示 WMI 事件跟踪结构。 您可以将显示范围限制为特定跟踪会话的结构。

```dbgcmd
!wmitrace.strdump [ LoggerID | LoggerName ] 
```

## <a name="span-idddk__wmitrace_strdump_dbgspanspan-idddk__wmitrace_strdump_dbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>参数


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span>*LoggerID*   
将显示范围限制为指定跟踪会话的事件跟踪结构。 *LoggerID* 指定跟踪会话。 它是系统分配给计算机上每个跟踪会话的序号。 如果未指定任何参数，则显示所有跟踪会话。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span>*LoggerName*   
将显示范围限制为指定跟踪会话的事件跟踪结构。 *LoggerName* 是启动跟踪会话时指定的文本名称。 如果未指定任何参数，则显示所有跟踪会话。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展由 Wmitrace.dll 导出。

此扩展在 windows 2000 和更高版本的 Windows 中可用。 如果要将此扩展与 Windows 2000 一起使用，必须先将 Wmitrace.dll 文件从 Windows 的调试工具安装目录的 winxp 子目录复制到 w2kfre 子目录。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关事件跟踪的概念性概述，请参阅 Microsoft Windows SDK。 有关 Tracelog 的信息，请参阅 Windows 驱动程序工具包 (WDK) 中的 "Tracelog" 主题。

<a name="remarks"></a>备注
-------

若要查找跟踪会话的记录器 ID，请使用 **！ wmitrace** 扩展名。 另外，还可以使用 Tracelog 命令 Tracelog-l 来列出跟踪会话及其基本属性，其中包括记录器 ID。

 

 





