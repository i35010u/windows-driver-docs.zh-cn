---
title: wmitrace.enable
description: Wmitrace.enable 扩展为指定的事件跟踪 Windows (ETW) 跟踪会话启用提供程序。
ms.assetid: 5a27fa00-7d52-43f7-84f4-82c5b5af1c06
keywords:
- wmitrace.enable Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.enable
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 99385a9e0e07abbd7cc60a6b864bdac3c29215a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332116"
---
# <a name="wmitraceenable"></a>!wmitrace.enable


**！ Wmitrace.enable**扩展为指定的事件跟踪 Windows (ETW) 跟踪会话启用提供程序。

```dbgcmd
!wmitrace.enable { LoggerID | LoggerName } GUID [-level Num] [-matchallkw Num] [-matchanykw Num] [-enableproperty Num] [-flag Num] 
```

## <a name="span-idddkwmitracestrdumpdbgspanspan-idddkwmitracestrdumpdbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>参数


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
指定跟踪会话。 *LoggerID*是一个系统将分配到计算机上每个跟踪会话的序号。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
指定跟踪会话。 *LoggerName*时的文本名称为指定开始跟踪会话时。

<span id="_______GUID______"></span><span id="_______guid______"></span> *GUID*   
指定要启用的提供程序 GUID。

<span id="_______-level_______Num______"></span><span id="_______-level_______num______"></span><span id="_______-LEVEL_______NUM______"></span> **-level** *Num*   
指定的级别。 *Num*可以是任何整数。

<span id="_______-matchallkw_______Num______"></span><span id="_______-matchallkw_______num______"></span><span id="_______-MATCHALLKW_______NUM______"></span> **-matchallkw** *Num*   
指定一个或多个关键字。 如果指定了多个关键字，仅当所有关键字均都匹配，将启用该提供程序。 *Num*可以是任何整数。

<span id="_______-matchanykw_______Num______"></span><span id="_______-matchanykw_______num______"></span><span id="_______-MATCHANYKW_______NUM______"></span> **-matchanykw** *Num*   
指定一个或多个关键字。 如果指定了多个关键字，如果至少一个关键字匹配，则将启用的提供程序。 *Num*可以是任何整数。 此参数的效果与效果重叠的标志参数。

<span id="_______-enableproperty_______Num______"></span><span id="_______-enableproperty_______num______"></span><span id="_______-ENABLEPROPERTY_______NUM______"></span> **-enableproperty** *Num*   
指定启用属性。 *Num*可以是任何整数。

<span id="_______-flag_______Num______"></span><span id="_______-flag_______num______"></span><span id="_______-FLAG_______NUM______"></span> **-flag** *Num*   
指定一个或多个标志。 *Num*可以是任何整数。 此参数的效果与-matchanykw 参数的效果重叠。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows 7 和更高版本的 Windows 中可用。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK。 有关跟踪工具的信息，请参阅 Windows Driver Kit (WDK)。

<a name="remarks"></a>备注
-------

使用此扩展插件之后, 必须继续执行程序 (例如，通过使用[ **g （转向）** ](g--go-.md)命令)，使其生效。 在很短的时间之后, 目标计算机自动进入调试器再次中断。

若要禁用某个提供程序，请使用[ **！ wmitrace.disable**](-wmitrace-disable.md)。

 

 





