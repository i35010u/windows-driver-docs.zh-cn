---
title: wmitrace
description: Wmitrace 扩展停止目标计算机上的 Windows (ETW 事件跟踪) 记录器。
keywords:
- wmitrace Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.stop
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9cd499b96d91797007aa5ff4e099eb0b335bf88a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819363"
---
# <a name="wmitracestop"></a>!wmitrace.stop


**！ Wmitrace** extension 停止目标计算机上的 WINDOWS (ETW 事件跟踪) 记录器。

```dbgcmd
!wmitrace.stop { LoggerID | LoggerName } 
```

## <a name="span-idddk__wmitrace_strdump_dbgspanspan-idddk__wmitrace_strdump_dbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>参数


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span>*LoggerID*   
指定跟踪会话。 *LoggerID* 是系统分配给计算机上每个跟踪会话的序号。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span>*LoggerName*   
指定跟踪会话。 *LoggerName* 是启动跟踪会话时指定的文本名称。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展由 Wmitrace.dll 导出。

Windows 7 和更高版本的 Windows 中提供了此扩展。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关事件跟踪的概念性概述，请参阅 Microsoft Windows SDK。 有关跟踪工具的信息，请参阅 Windows 驱动程序工具包 (WDK) 。

<a name="remarks"></a>备注
-------

使用此扩展后，你必须继续执行程序 (例如，通过使用 [**g (转)**](g--go-.md) 命令) ，使其生效。 经过一段时间后，目标计算机会自动中断到调试器。

若要启动 ETW 记录器，请使用 [**！ wmitrace**](-wmitrace-start.md)。

 

 





