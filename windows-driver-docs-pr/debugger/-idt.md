---
title: idt
description: Idt 扩展显示为指定的中断调度表 (IDT) 中断服务例程 (Isr)。
ms.assetid: 6b289fde-85a3-4a40-8354-db6861ca8cb2
keywords:
- ISR （中断服务例程）
- IDT （中断调度表）
- idt Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- idt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c65570198a00701ea15c301c1afeb15ed535525b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336466"
---
# <a name="idt"></a>!idt


**！ Idt**扩展显示为指定的中断调度表 (IDT) 中断服务例程 (Isr)。

```dbgcmd
!idt IDT 
!idt [-a] 
!idt -? 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______IDT______"></span><span id="_______idt______"></span> *IDT*   
指定要显示 IDT。

<span id="_______-a______"></span><span id="_______-A______"></span> **-a**   
当*IDT*未指定，则调试器将显示所有处理器的 IDTs 以缩写格式在目标计算机上。 如果 **-a**指定，则为每个 IDT Isr 也会显示。

<span id="_______-_______"></span> **-?**   
显示此扩展在调试器命令窗口中的帮助。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

此扩展命令仅用于基于 x64 或基于 x86 的目标计算机。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关 Isr 和 IDTs 的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

有关如何在 Itanium 的目标计算机上显示中断向量表的详细信息，请参阅[ **！ 程序**](-ivt.md)。

<a name="remarks"></a>备注
-------

下面是输出的来自此扩展插件示例：

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

 

 





