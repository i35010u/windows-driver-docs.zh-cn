---
title: wdfkd.wdfpoolusage
description: 如果驱动程序启用了内核模式驱动程序框架 (KMDF) 验证工具，wdfkd.wdfpoolusage 扩展显示指定驱动程序，池使用情况的信息。
ms.assetid: 6a77b76b-c970-447c-a8dd-e1ceb7add611
keywords:
- wdfkd.wdfpoolusage Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfpoolusage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a8c550d6c850fdfcc1acca8a46e0f409ccb038b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323263"
---
# <a name="wdfkdwdfpoolusage"></a>!wdfkd.wdfpoolusage


**！ Wdfkd.wdfpoolusage**扩展显示的指定驱动程序，池使用情况信息，如果驱动程序启用了内核模式驱动程序框架 (KMDF) 验证程序。

```dbgcmd
!wdfkd.wdfpoolusage [DriverName [SearchAddress] [Flags]]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *DriverName*   
可选。 驱动程序的名称。 *DriverName*不得包含.sys 文件扩展名。

<span id="_______SearchAddress______"></span><span id="_______searchaddress______"></span><span id="_______SEARCHADDRESS______"></span> *SearchAddress*   
可选。 一个字符串，表示内存地址。 包含池项*SearchAddress*显示。 如果*SearchAddress*为 0 或省略，所有驱动程序的池条目会显示。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 要显示的信息类型。 此参数才有效才*SearchAddress*为非零值。 *标志*可以是以下位的任意组合。 默认值为 0x0。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示详细输出。 每个显示多个行。 如果未设置此标志，在一行上显示有关分配的信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示内部键入每个句柄的信息。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
显示每个池项的调用方。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

如果省略*DriverName*使用参数，默认驱动程序。 可通过使用显示的默认驱动程序[ **！ wdfkd.wdfgetdriver** ](-wdfkd-wdfgetdriver.md)扩展; 您可以通过使用设置的默认驱动程序[ **！ wdfkd.wdfsetdriver**](-wdfkd-wdfsetdriver.md)扩展。

下面的示例演示的输出 **！ wdfpoolusage**扩展不标记任何池分配时，*标志*值设置为 0。

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

下面的示例演示的输出 **！ wdfpoolusage**时出现的值*标志*为 1。 （请注意，在第二行的省略号 （...） 指示省略一些与前面的示例中所示相同的输出。）

```dbgcmd
kd> !wdfpoolusage wdfrawbusenumtest 0 1 
. . . 
100 PeakNonPaged Allocations, 14 PeakPaged Allocations

Client alloc starts at 82dbae00
Size  512 Tag 'RawB'
NonPaged (0x0)
Caller:  Wdf01000!FxVerifierLock::AllocateThreadTable+5d
```

 

 





