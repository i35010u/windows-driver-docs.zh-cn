---
title: idt
description: Idt 扩展显示)  (的中断服务例程 (IDT) 的指定中断调度表。
ms.assetid: 6b289fde-85a3-4a40-8354-db6861ca8cb2
keywords:
- 'ISR (中断服务例程) '
- 'IDT (中断调度表) '
- idt Windows 调试
ms.date: 05/13/2020
topic_type:
- apiref
api_name:
- idt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 69afcb7baf46c911eeddcbac8930a505f1050397
ms.sourcegitcommit: bb3b62a57ba3aea4a0adeefd2d81993367b7b334
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88148458"
---
# <a name="idt"></a>!idt


**！ Idt** extension 显示 (idt) 的指定中断调度表 (isr) 的中断服务例程。

```dbgcmd
!idt IDT 
!idt [-a] 
!idt -? 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______IDT______"></span><span id="_______idt______"></span>*IDT*   
指定要显示的 IDT。

<span id="_______-a______"></span><span id="_______-A______"></span>**-a**   
如果未指定 *IDT* ，则调试器将以缩写格式显示目标计算机上的所有处理器的 IDTs。 如果指定 **-a** ，则还会显示每个 IDT 的 isr。

<span id="_______-_______"></span> **-?**   
在调试器中显示此扩展的帮助命令窗口。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Unavailable</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

此扩展命令只能与基于 x64 或基于 x86 的目标计算机一起使用。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 Isr 和 IDTs 的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部* ，并标记 Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

下面是此扩展的输出示例：

```dbgcmd
0: kd> !idt

Dumping IDT:

37:806ba78c hal!PicSpuriousService37
3d:806bbc90 hal!HalpApcInterrupt
41:806bbb04 hal!HalpDispatchInterrupt
50:806ba864 hal!HalpApicRebootService
63:8641376c VIDEOPRT!pVideoPortInterrupt (KINTERRUPT 86413730)
73:862aa044 portcls!CInterruptSyncServiceRoutine (KINTERRUPT 862aa008)
82:86594314 atapi!IdePortInterrupt (KINTERRUPT 865942d8)
83:86591bec SCSIPORT!ScsiPortInterrupt (KINTERRUPT 86591bb0)
92:862b53dc serial!SerialCIsrSw (KINTERRUPT 862b53a0)
93:86435844 i8042prt!I8042KeyboardInterruptService (KINTERRUPT 86435808)
a3:863b366c i8042prt!I8042MouseInterruptService (KINTERRUPT 863b3630)
a4:8636bbec USBPORT!USBPORT_InterruptService (KINTERRUPT 8636bbb0)
b1:86585bec ACPI!ACPIInterruptServiceRoutine (KINTERRUPT 86585bb0)
b2:863c0524 serial!SerialCIsrSw (KINTERRUPT 863c04e8)
b4:86391a54 NDIS!ndisMIsr (KINTERRUPT 86391a18)
         USBPORT!USBPORT_InterruptService (KINTERRUPT 863ae890)
c1:806ba9d0 hal!HalpBroadcastCallService
d1:806b9dd4 hal!HalpClockInterrupt
e1:806baf30 hal!HalpIpiHandler
e3:806baca8 hal!HalpLocalApicErrorService
fd:806bb460 hal!HalpProfileInterrupt
```

 

 





