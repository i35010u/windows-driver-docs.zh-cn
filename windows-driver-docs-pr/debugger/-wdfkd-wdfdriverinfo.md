---
title: wdfkd.wdfdriverinfo
description: Wdfkd.wdfdriverinfo 扩展显示有关指定的驱动程序，包括其设备树中，信息和版本信息。
ms.assetid: dc758fd3-1226-46e3-b249-2cf37ef3e539
keywords:
- wdfkd.wdfdriverinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfdriverinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 675b7f1eea24bd62561f53896033d9f0b3bf5496
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554055"
---
# <a name="wdfkdwdfdriverinfo"></a>!wdfkd.wdfdriverinfo


**！ Wdfkd.wdfdriverinfo**扩展显示有关指定的驱动程序，包括其设备树、 驱动程序用，编译的内核模式驱动程序框架 (KMDF) 库的版本和一系列的信息framework 设备驱动程序创建的对象。

```dbgcmd
!wdfkd.wdfdriverinfo [DriverName [Flags]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *DriverName*   
可选。 驱动程序的名称。 *DriverName*不得包含.sys 文件扩展名。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示的信息类型的标志。 *标志*可以是以下位的任意组合：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示将包括驱动程序验证器设置，并且还将包括 WDF 对象的计数。 此标志可以结合位 6 (0x40) 以显示内部对象。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
显示将包含该驱动程序的 KMDF 句柄层次结构。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>5 位 (0x20)  
显示将包含每个句柄的上下文和回调函数信息。 此标志是有效的仅当位 4 设置 (0x10)。

<span id="Bit_6__0x40_"></span><span id="bit_6__0x40_"></span><span id="BIT_6__0X40_"></span>第 6 位 (0x40)  
显示将包含每个句柄的其他信息。 此标志是有效的仅当位 4 设置 (0x10)。 此标志可以结合位 0 (0x1) 以显示内部对象。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>7 位 (0x80)  
将更紧凑的形式显示的句柄信息。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>位 8 (0x100)  
显示将左对齐的内部类型信息。 此标志是有效的仅当位 4 设置 (0x10)。

<span id="Bit_9__0x200_"></span><span id="bit_9__0x200_"></span><span id="BIT_9__0X200_"></span>9 (0x200) 位  
显示将包含该驱动程序可能会泄漏的句柄。 KMDF 1.1 及更高版本支持此标志。 此标志是有效的仅当位 4 设置 (0x10)。

<span id="Bit_10__0x400_"></span><span id="bit_10__0x400_"></span><span id="BIT_10__0X400_"></span>位 10 (0x400)  
在详细窗体中显示将包含设备树。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

如果省略*DriverName*使用参数，默认驱动程序。 可通过使用显示的默认驱动程序[ **！ wdfkd.wdfgetdriver** ](-wdfkd-wdfgetdriver.md)扩展; 您可以通过使用设置的默认驱动程序[ **！ wdfkd.wdfsetdriver**](-wdfkd-wdfsetdriver.md)扩展。

下面的示例演示从显示 **！ wdfkd.wdfdriverinfo**扩展。

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

 

 





