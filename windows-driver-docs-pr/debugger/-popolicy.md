---
title: popolicy
description: Popolicy 扩展显示目标计算机的电源策略。
keywords:
- popolicy Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- popolicy
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 986560a0c897482e5c640f75360fcd4e648b4691
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791699"
---
# <a name="popolicy"></a>!popolicy


**！ Popolicy** extension 显示目标计算机的电源策略。

```dbgcmd
!popolicy [Address]
```

## <a name="span-idddk__popolicy_dbgspanspan-idddk__popolicy_dbgspanparameters"></a><span id="ddk__popolicy_dbg"></span><span id="DDK__POPOLICY_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示的电源策略结构的地址。 如果省略，则 nt！将显示 PopPolicy。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

若要查看系统的电源功能，请使用 [**！ pocaps**](-pocaps.md) extension 命令。 有关电源功能和电源策略的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部*，并将 Russinovich 和 David 所罗门群岛标记为。

<a name="remarks"></a>备注
-------

下面是此命令的输出示例：

```dbgcmd
kd> !popolicy
SYSTEM_POWER_POLICY (R.1) @ 0x80164d58
  PowerButton:      Shutdown  Flags: 00000003   Event: 00000000   Query UI
  SleepButton:          None  Flags: 00000003   Event: 00000000   Query UI
  LidClose:             None  Flags: 00000001   Event: 00000000   Query
  Idle:                 None  Flags: 00000001   Event: 00000000   Query
  OverThrottled:        None  Flags: c0000004   Event: 00000000   Override NoWakes Critical
  IdleTimeout:             0  IdleSensitivity:        50%
  MinSleep:               S0  MaxSleep:               S0
  LidOpenWake:            S0  FastSleep:              S0
  WinLogonFlags:           1  S4Timeout:               0
  VideoTimeout:            0  VideoDim:               209
  SpinTimeout:             0  OptForPower:             1
  FanTolerance:            0% ForcedThrottle:          0%
  MinThrottle:             0%
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[即插即用和 Power 调试器命令](plug-and-play-and-power-debugger-commands.md)

 

 






