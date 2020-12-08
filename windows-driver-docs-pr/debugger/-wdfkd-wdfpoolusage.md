---
title: wdfkd.wdfpoolusage
description: 如果为驱动程序启用了 Kernel-Mode Driver Framework (KMDF) 验证程序，则 wdfpoolusage 扩展将显示指定驱动程序的池使用情况信息。
keywords:
- wdfkd wdfpoolusage Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfpoolusage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d5e4702657be77618024e3e59ce21dbf55aef999
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833721"
---
# <a name="wdfkdwdfpoolusage"></a>!wdfkd.wdfpoolusage


如果为驱动程序启用了 Kernel-Mode Driver Framework (KMDF) 验证程序 **，则会** 显示指定驱动程序的池使用情况信息。

```dbgcmd
!wdfkd.wdfpoolusage [DriverName [SearchAddress] [Flags]]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span>*DriverName*   
可选。 驱动程序的名称。 *DriverName* 不得包含 .sys 文件扩展名。

<span id="_______SearchAddress______"></span><span id="_______searchaddress______"></span><span id="_______SEARCHADDRESS______"></span>*SearchAddress*   
可选。 表示内存地址的字符串。 将显示包含 *SearchAddress* 的池条目。 如果 *SearchAddress* 为0或省略，则显示所有驱动程序的池条目。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 要显示的信息的类型。 仅当 *SearchAddress* 为非零值时，此参数才有效。 *标志* 可以是以下位的任意组合。 默认值为0x0。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示详细输出。 为每个显示多个行。 如果未设置此标志，则会在一行上显示有关分配的信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
显示每个句柄的内部类型信息。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
显示每个池项的调用方。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

如果省略 *DriverName* 参数，则使用默认的驱动程序。 可以使用 [**！ wdfkd; wdfgetdriver**](-wdfkd-wdfgetdriver.md) 扩展显示默认驱动程序;可以使用 [**！ wdfkd. wdfsetdriver**](-wdfkd-wdfsetdriver.md) 扩展设置默认驱动程序。

下面的示例演示了在未标记池分配并且 *Flags* 值设置为0时， **！ wdfpoolusage** 扩展的输出。

```dbgcmd
## kd> !wdfpoolusage wdfrawbusenumtest 0 0 
-----------------------------------
## FxDriverGlobals 83b7af18 pool stats
-----------------------------------
Driver Tag: 'RawB'
15126 NonPaged Bytes, 548 Paged Bytes
94 NonPaged Allocations, 10 Paged Allocations
15610 PeakNonPaged Bytes, 752 PeakPaged Bytes
100 PeakNonPaged Allocations, 14 PeakPaged Allocations

pool 82dbae00, Size  512 Tag 'RawB', NonPaged, Caller:  Wdf01000!FxVerifierLock::AllocateThreadTable+5d
```

下面的示例演示了在 *Flags* 值为1时显示的 **！ wdfpoolusage** 的输出。  (请注意，第二行的省略号 ( ... ) 指示省略了与前面的示例中所示相同的输出。 ) 

```dbgcmd
kd> !wdfpoolusage wdfrawbusenumtest 0 1 
. . . 
100 PeakNonPaged Allocations, 14 PeakPaged Allocations

Client alloc starts at 82dbae00
Size  512 Tag 'RawB'
NonPaged (0x0)
Caller:  Wdf01000!FxVerifierLock::AllocateThreadTable+5d
```

 

 





