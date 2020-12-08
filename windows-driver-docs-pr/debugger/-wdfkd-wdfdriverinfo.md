---
title: wdfkd.wdfdriverinfo
description: Wdfkd. wdfdriverinfo 扩展显示有关指定驱动程序的信息，包括其设备树和版本信息。
keywords:
- wdfkd wdfdriverinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfdriverinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de6ba0c2634f18cee2245791034ae5005b2f7615
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833203"
---
# <a name="wdfkdwdfdriverinfo"></a>!wdfkd.wdfdriverinfo


**！ Wdfkd wdfdriverinfo** 扩展显示有关指定驱动程序的信息，包括其设备树、驱动程序所用的 Kernel-Mode driver FRAMEWORK (KMDF) 库的版本，以及驱动程序创建的框架设备对象的列表。

```dbgcmd
!wdfkd.wdfdriverinfo [DriverName [Flags]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span>*DriverName*   
可选。 驱动程序的名称。 *DriverName* 不得包含 .sys 文件扩展名。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 用于指定要显示的信息类型的标志。 *标志* 可以是以下位的任意组合：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示将包括驱动程序的验证程序设置，还将包含 WDF 对象的计数。 此标志可以与第6个 (0x40 ") 组合以显示内部对象。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)   
显示将包括驱动程序的 KMDF 句柄层次结构。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>第 5 (0x20)   
显示将包括每个句柄的上下文和回调函数信息。 仅当设置了位 4 (0x10) 时，此标志才有效。

<span id="Bit_6__0x40_"></span><span id="bit_6__0x40_"></span><span id="BIT_6__0X40_"></span>第 6 (0x40)   
显示内容将包含每个句柄的附加信息。 仅当设置了位 4 (0x10) 时，此标志才有效。 此标志可以与位 0 (0x1) 组合以显示内部对象。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>第7位 (0x80)   
句柄信息将以更简洁的格式显示。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>位 8 (0x100)   
显示将左对齐内部类型信息。 仅当设置了位 4 (0x10) 时，此标志才有效。

<span id="Bit_9__0x200_"></span><span id="bit_9__0x200_"></span><span id="BIT_9__0X200_"></span>第 9 (0x200)   
显示将包括驱动程序可能泄露的句柄。 KMDF 版本1.1 和更高版本支持此标志。 仅当设置了位 4 (0x10) 时，此标志才有效。

<span id="Bit_10__0x400_"></span><span id="bit_10__0x400_"></span><span id="BIT_10__0X400_"></span>位 10 (0x400)   
显示将以详细形式包含设备树。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

如果省略 *DriverName* 参数，则使用默认的驱动程序。 可以使用 [**！ wdfkd; wdfgetdriver**](-wdfkd-wdfgetdriver.md) 扩展显示默认驱动程序;可以使用 [**！ wdfkd. wdfsetdriver**](-wdfkd-wdfsetdriver.md) 扩展设置默认驱动程序。

下面的示例演示了 **！ wdfkd. wdfdriverinfo** 扩展中的显示。

```dbgcmd
## kd> !wdfdriverinfo wdfrawbusenumtest 
----------------------------------
Default driver image name:   wdfrawbusenumtest
WDF library image name:      Wdf01000
 FxDriverGlobals  0x83b7af18
 WdfBindInfo      0xf22250ec
##    Version        v1.5 build(1234)
----------------------------------
WDFDRIVER: 0x7cbc90d0

    !WDFDEVICE 0x7ca7b1c0
            context:  dt 0x83584ff8 ROOT_CONTEXT (size is 0x1 bytes)
             <no associated attribute callbacks>

    !WDFDEVICE 0x7cad31c8
            context:  dt 0x8352cff0 RAW_PDO_CONTEXT (size is 0xc bytes)
             <no associated attribute callbacks>
```

 

 





