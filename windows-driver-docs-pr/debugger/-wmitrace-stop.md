---
title: wmitrace.stop
description: Wmitrace.stop 扩展停止目标计算机上的事件跟踪 Windows (ETW) 记录器。
ms.assetid: 38be65ae-efef-400f-bb10-315d1f6b11d8
keywords:
- wmitrace.stop Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.stop
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5405cdff8afb78fede95f8532a77aa69db146f76
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331054"
---
# <a name="wmitracestop"></a>!wmitrace.stop


**！ Wmitrace.stop**扩展在目标计算机上停止事件跟踪 Windows (ETW) 记录器。

```dbgcmd
!wmitrace.stop { LoggerID | LoggerName } 
```

## <a name="span-idddkwmitracestrdumpdbgspanspan-idddkwmitracestrdumpdbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>参数


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
指定跟踪会话。 *LoggerID*是一个系统将分配到计算机上每个跟踪会话的序号。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
指定跟踪会话。 *LoggerName*时的文本名称为指定开始跟踪会话时。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows 7 和更高版本的 Windows 中可用。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK。 有关跟踪工具的信息，请参阅 Windows Driver Kit (WDK)。

<a name="remarks"></a>备注
-------

使用此扩展插件之后, 必须继续执行程序 (例如，通过使用[ **g （转向）** ](g--go-.md)命令)，使其生效。 在很短的时间之后, 目标计算机自动进入调试器再次中断。

若要启动 ETW 记录器，请使用[ **！ wmitrace.start**](-wmitrace-start.md)。

 

 





