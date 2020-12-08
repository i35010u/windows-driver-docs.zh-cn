---
title: powertriage
description: Powertriage 扩展显示有关系统和设备电源相关组件的摘要信息。
keywords:
- powertriage Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- powertriage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f6ebe76edccc51e378836c46f4703aeb506fc3a3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791695"
---
# <a name="powertriage"></a>!powertriage


！ Powertriage 扩展显示有关系统和设备电源相关组件的摘要信息。 它还提供指向可用于收集其他信息的相关命令的链接。 ！ Powertriage 命令没有参数。 此命令可用于实时内核模式调试和故障转储文件分析。

语法

```dbgcmd
!powertriage
```

## <a name="span-idddk__thread_dbgspanspan-idddk__thread_dbgspanparameters"></a><span id="ddk__thread_dbg"></span><span id="DDK__THREAD_DBG"></span>参数


无

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 10 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

！ Powertriage 扩展显示以下信息。

1. 所有设备对象的设备节点的电源状态以及！ podev。
2. 如果驱动程序已启用 IFR，则链接到 [**！ rcdrkd. rcdrlogdump。**](-rcdrkd-rcdrlogdump.md) 有关 IFR 的详细信息，请参阅 [在 KMDF 和 UMDF 2 驱动程序中使用即时 Trace 录像机 (IFR) ](../wdf/using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers.md)。
3. 指向 WDF 驱动程序的 [**！ wdfkd. wdfdriverinfo**](-wdfkd-wdfdriverinfo.md) 和 [**！ wdfkd**](-wdfkd-wdflogdump.md) 的链接。
4. 链接到！ fxdevice for PoFx 设备。 有关 PoFX 的详细信息，请参阅 [电源管理框架概述](../kernel/overview-of-the-power-management-framework.md)。
下面是！ powertriage 命令的示例输出。

```dbgcmd
kd> !powertriage

System Capabilities :
  Machine is not AOAC capable.

Power Capabilities:
PopCapabilities @ 0xfffff8022f6c4380
  Misc Supported Features:  PwrButton S1 S3 S4 S5 HiberFile FullWake
  Processor Features:      
  Disk Features:           
  Battery Features:        
  Wake Caps
    Ac OnLine Wake:         Sx
    Soft Lid Wake:          Sx
    RTC Wake:               S4
    Min Device Wake:        Sx
    Default Wake:           Sx



Power Action:

PopAction :fffff8022f6ba550
    Current System State..: Working
    Target System State...: Unspecified
    State.................: - Idle(0)

Devices with allocated Power IRPs:

    +  ACPI\PNP0C0C\2&daba3ff&1
       0xffffe00023939ad0 ACPI D0 !podev  WAIT_WAKE_IRP !irp Related Threads 

    +  USB\ROOT_HUB30\5&2c60645a&0&0
       0xffffe0002440ac40 USBXHCI D2 !podev  WAIT_WAKE_IRP !irp Related Threads !rcdrlogdump !wdfdriverinfo !wdflogdump 
         Upper DO 0xffffe00024415a10 USBHUB3 !podev 


    +  USB\ROOT_HUB30\5&d91dce5&0&0
       0xffffe00023ed4d30 USBXHCI D2 !podev  WAIT_WAKE_IRP !irp Related Threads !rcdrlogdump !wdfdriverinfo !wdflogdump 
         Upper DO 0xffffe000249d8040 USBHUB3 !podev 

    +  PCI\VEN_8086&DEV_27E2&SUBSYS_01DE1028&REV_01\3&172e68dd&0&E5
       0xffffe000239e5880 pci D0 !podev FxDevice: !fxdevice  WAIT_WAKE_IRP !irp Related Threads 
         Upper DO 0xffffe000239c0e50 ACPI !podev 
           Upper DO 0xffffe000239f7040 pci !podev 


    +  PCI\VEN_14E4&DEV_167A&SUBSYS_01DE1028&REV_02\4&24ac2e11&0&00E5
       0xffffe000231e6060 pci D0 !podev  WAIT_WAKE_IRP !irp Related Threads 
         Upper DO 0xffffe00024359050 b57nd60a !podev 


Device Tree Info: 

    !devpowerstate

    !devpowerstate Complete


Links:
!poaction
!cstriage
!pdctriage
!pdcclients
!fxdevice
!pnptriage
```

**转储文件电源故障分析**

在检查与错误电源状态信息相关的系统崩溃时，！ powertriage 扩展可能很有用。 例如，在发生 [**错误检查0x9F：驱动程序 \_ 电源 \_ 状态 \_ 故障**](bug-check-0x9f--driver-power-state-failure.md)的情况下，该扩展将显示所有已分配的电源 irp，相关联的设备堆栈连同：

1. 链接到相关 Irp 的 [**！ irp**](-irp.md) 命令。
2. 指向带有相关 IRP 的 [**！ findthreads**](-findthreads.md) 命令的链接。 IRP 作为搜索条件的一部分进行添加，并将以更高的相关性开始的线程显示到前面列出的搜索条件线程。
用 power Irp 转储所有设备堆栈可帮助进行调试，其中！分析无法正确标识与崩溃关联的 IRP。

 

