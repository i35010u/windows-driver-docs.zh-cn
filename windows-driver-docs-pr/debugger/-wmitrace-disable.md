---
title: wmitrace.disable
description: Wmitrace.disable 扩展为指定的事件跟踪 Windows (ETW) 跟踪会话禁用某个提供程序。
ms.assetid: b993bfa4-2d3d-4739-9d5e-0cb714369742
keywords:
- wmitrace.disable Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.disable
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4fb49cbd5fcf8b1fc1139e7601b8644458b3e379
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555497"
---
# <a name="wmitracedisable"></a>!wmitrace.disable


**！ Wmitrace.disable**扩展为指定的事件跟踪 Windows (ETW) 跟踪会话禁用某个提供程序。

```dbgcmd
!wmitrace.disable { LoggerID | LoggerName } GUID 
```

## <a name="span-idddkwmitracestrdumpdbgspanspan-idddkwmitracestrdumpdbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>参数


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
指定跟踪会话。 *LoggerID*是一个系统将分配到计算机上每个跟踪会话的序号。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
指定跟踪会话。 *LoggerName*时的文本名称为指定开始跟踪会话时。

<span id="_______GUID______"></span><span id="_______guid______"></span> *GUID*   
指定要禁用的提供程序 GUID。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows 7 和更高版本的 Windows 中可用。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK。 有关跟踪工具的信息，请参阅 Windows Driver Kit (WDK)。

<a name="remarks"></a>备注
-------

使用此扩展插件之后, 必须继续执行程序 (例如，通过使用[ **g （转向）** ](g--go-.md)命令)，使其生效。 在很短的时间之后, 目标计算机自动进入调试器再次中断。

若要启用提供程序，请使用[ **！ wmitrace.enable**](-wmitrace-enable.md)。

 

 





