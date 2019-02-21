---
title: powertriage
description: 有关系统和设备电源 powertriage 扩展显示摘要信息相关组件。
ms.assetid: A202ED64-B706-42AC-B058-C44321C9171F
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
ms.openlocfilehash: 90a760ab85eb0a5ea9b484754eb987dbd2c2a7da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524881"
---
# <a name="powertriage"></a>！ powertriage


！ Powertriage 扩展显示摘要信息系统和设备电源相关的组件。 它还提供了指向可用于收集的其他信息的相关命令。 ！ Powertriage 命令不具有任何参数。 可以使用此命令，以及这两个实时内核模式调试和故障转储文件分析。

语法

```dbgcmd
!powertriage
```

## <a name="span-idddkthreaddbgspanspan-idddkthreaddbgspanparameters"></a><span id="ddk__thread_dbg"></span><span id="DDK__THREAD_DBG"></span>参数


无

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

！ Powertriage 扩展将显示以下信息。

1. 电源和设备节点的状态 ！ podev 的所有设备对象。
2. 链接到[ **！ rcdrkd.rcdrlogdump** ](-rcdrkd-rcdrlogdump.md)如果驱动程序已启用 IFR。 有关 IFR 详细信息，请参阅[使用即时跟踪记录器 (IFR) KMDF 和 UMDF 2 驱动程序中](https://msdn.microsoft.com/library/windows/hardware/dn940485)。
3. 链接到[ **！ wdfkd.wdfdriverinfo** ](-wdfkd-wdfdriverinfo.md)并[ **！ wdfkd.wdflogdump** ](-wdfkd-wdflogdump.md) WDF 驱动程序。
4. 链接到 ！ fxdevice PoFx 设备。 有关 PoFX 详细信息，请参阅[电源管理框架概述](https://msdn.microsoft.com/library/windows/hardware/hh406637)。
下面是示例输出 ！ powertriage 命令。

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

！ Powertriage 扩展可用于检查相关错误的电源状态信息的系统崩溃。 例如，在中的情况下[ **Bug 检查 0x9F:驱动程序\_电源\_状态\_失败**](bug-check-0x9f--driver-power-state-failure.md)，扩展将显示所有已分配的 power Irp，连同关联的设备堆栈：

1. 链接到[ **！ irp** ](-irp.md)相关 Irp 命令。
2. 链接到[ **！ findthreads** ](-findthreads.md)相关 IRP 命令。 IRP 添加为该搜索条件并显示从开始到搜索条件线程更高版本关联的线程首先列出的一部分。
转储的 power Irp 可帮助在调试中的所有设备堆栈事例 ！ 分析无法以正确地标识 IRP 与故障相关联。

 

 





