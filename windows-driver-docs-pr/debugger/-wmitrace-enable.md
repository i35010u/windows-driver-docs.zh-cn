---
title: wmitrace
description: Wmitrace 扩展为 Windows (ETW) trace 会话启用指定的事件跟踪的提供程序。
keywords:
- wmitrace Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.enable
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f06808860b4db5f29979e3a44fbd597793c3f0f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823543"
---
# <a name="wmitraceenable"></a>!wmitrace.enable


**！ Wmitrace** 扩展为 WINDOWS (ETW) trace 会话的指定事件跟踪启用提供程序。

```dbgcmd
!wmitrace.enable { LoggerID | LoggerName } GUID [-level Num] [-matchallkw Num] [-matchanykw Num] [-enableproperty Num] [-flag Num] 
```

## <a name="span-idddk__wmitrace_strdump_dbgspanspan-idddk__wmitrace_strdump_dbgspanparameters"></a><span id="ddk__wmitrace_strdump_dbg"></span><span id="DDK__WMITRACE_STRDUMP_DBG"></span>参数


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span>*LoggerID*   
指定跟踪会话。 *LoggerID* 是系统分配给计算机上每个跟踪会话的序号。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span>*LoggerName*   
指定跟踪会话。 *LoggerName* 是启动跟踪会话时指定的文本名称。

<span id="_______GUID______"></span><span id="_______guid______"></span>*GUID*   
指定要启用的提供程序的 GUID。

<span id="_______-level_______Num______"></span><span id="_______-level_______num______"></span><span id="_______-LEVEL_______NUM______"></span>**-级别** *Num*   
指定级别。 *Num* 可以是任意整数。

<span id="_______-matchallkw_______Num______"></span><span id="_______-matchallkw_______num______"></span><span id="_______-MATCHALLKW_______NUM______"></span>**-matchallkw** *Num*   
指定一个或多个关键字。 如果指定了多个关键字，则只有在所有关键字都匹配时才会启用提供程序。 *Num* 可以是任意整数。

<span id="_______-matchanykw_______Num______"></span><span id="_______-matchanykw_______num______"></span><span id="_______-MATCHANYKW_______NUM______"></span>**-matchanykw** *Num*   
指定一个或多个关键字。 如果指定了多个关键字，则如果至少匹配一个关键字，则会启用提供程序。 *Num* 可以是任意整数。 此参数的效果与-标志参数的效果重叠。

<span id="_______-enableproperty_______Num______"></span><span id="_______-enableproperty_______num______"></span><span id="_______-ENABLEPROPERTY_______NUM______"></span>**-enableproperty** *Num*   
指定 enable 属性。 *Num* 可以是任意整数。

<span id="_______-flag_______Num______"></span><span id="_______-flag_______num______"></span><span id="_______-FLAG_______NUM______"></span>**-标志** *Num*   
指定一个或多个标志。 *Num* 可以是任意整数。 此参数的效果与-matchanykw 参数的效果重叠。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展由 Wmitrace.dll 导出。

Windows 7 和更高版本的 Windows 中提供了此扩展。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关事件跟踪的概念性概述，请参阅 Microsoft Windows SDK。 有关跟踪工具的信息，请参阅 Windows 驱动程序工具包 (WDK) 。

<a name="remarks"></a>备注
-------

使用此扩展后，你必须继续执行程序 (例如，通过使用 [**g (转)**](g--go-.md) 命令) ，使其生效。 经过一段时间后，目标计算机会自动中断到调试器。

若要禁用提供程序，请使用 [**！ wmitrace**](-wmitrace-disable.md)。

 

 





