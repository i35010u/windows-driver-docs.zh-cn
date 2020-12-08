---
title: wdfkd.wdfhandle
description: Wdfkd. wdfhandle 扩展显示有关指定框架对象句柄的信息，如句柄类型、对象上下文指针和基础框架对象指针。
keywords:
- wdfkd wdfhandle Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfhandle
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 90c087e2e0841e87ef6814c1363579a9cf997472
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838393"
---
# <a name="wdfkdwdfhandle"></a>!wdfkd.wdfhandle


**！ Wdfkd wdfhandle** 扩展显示有关指定框架对象句柄的信息，如句柄类型、对象上下文指针和基础框架对象指针。

```dbgcmd
!wdfkd.wdfhandle Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
框架对象的句柄。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 用于指定要显示的信息类型的标志。 *标志* 可以是以下位的任意组合。 默认值为0x0。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)   
显示将包括指定句柄的子对象的子树。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>第 5 (0x20)   
显示内容将包括指定句柄的上下文和回调函数信息。 仅当设置了位 4 (0x10) 时，此标志才有效。

<span id="Bit_6__0x40_"></span><span id="bit_6__0x40_"></span><span id="BIT_6__0X40_"></span>第 6 (0x40)   
显示内容将包括指定句柄的其他信息。 仅当设置了位 4 (0x10) 时，此标志才有效。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>第7位 (0x80)   
句柄信息将以更简洁的格式显示。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>位 8 (0x100)   
显示将左对齐内部类型信息。 仅当设置了位 4 (0x10) 时，此标志才有效。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

下面的示例演示在 *Flags* 参数 (中设置了位4的 **！ wdfhandle** 扩展的输出，因此输出显示) 的子对象的相关信息。

```dbgcmd
kd> !wdfhandle 0x7ca7b1c0 10 

handle 0x7ca7b1c0, type is WDFDEVICE

Contexts:
    context:  dt 0x83584ff8 ROOT_CONTEXT (size is 0x1 bytes)
     <no associated attribute callbacks>

Child WDFHANDLEs of 0x7ca7b1c0:
    WDFDEVICE 0x7ca7b1c0
        WDFCMRESLIST 0x7ccfb058
        WDFCMRESLIST 0x7cadb058
        WDFCHILDLIST 0x7c72f0c8
        WDFCHILDLIST 0x7cc090c8
        WDFIOTARGET 0x7c9630b8

!wdfobject 0x83584e38
```

在前面的示例中，输入句柄引用了一个 WDFDEVICE 对象。 此特定设备对象具有五个子对象，即两个 WDFCMRESLIST 对象、两个 WDFCHILDLIST 对象和一个 WDFIOTARGET 对象。

 

 





