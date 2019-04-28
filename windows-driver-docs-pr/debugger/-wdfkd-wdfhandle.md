---
title: wdfkd.wdfhandle
description: Wdfkd.wdfhandle 扩展显示有关指定的框架对象句柄，例如句柄类型、 对象的上下文指针和基础框架对象指针的信息。
ms.assetid: 9365218e-2647-4e54-baba-8774d4ab3ae1
keywords:
- wdfkd.wdfhandle Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfhandle
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3d9070b24233fb5a1ed198bbe300ef6ec6deca24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341697"
---
# <a name="wdfkdwdfhandle"></a>!wdfkd.wdfhandle


**！ Wdfkd.wdfhandle**扩展显示有关指定的框架对象句柄，例如句柄类型信息对象的上下文指针和基础框架对象指针。

```dbgcmd
!wdfkd.wdfhandle Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
Framework 对象的句柄。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示的信息类型的标志。 *标志*可以是以下位的任意组合。 默认值为 0x0。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
显示将包含子对象的指定句柄的子的树。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>5 位 (0x20)  
显示将包含指定句柄的上下文和回调函数信息。 此标志是有效的仅当位 4 设置 (0x10)。

<span id="Bit_6__0x40_"></span><span id="bit_6__0x40_"></span><span id="BIT_6__0X40_"></span>第 6 位 (0x40)  
显示将包括指定句柄的其他信息。 此标志是有效的仅当位 4 设置 (0x10)。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>7 位 (0x80)  
将更紧凑的形式显示的句柄信息。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>位 8 (0x100)  
显示将左对齐的内部类型信息。 此标志是有效的仅当位 4 设置 (0x10)。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

下面的示例演示的输出 **！ wdfhandle**扩展插件设置的 4 位*标志*参数 （因此，输出会显示有关子对象的信息）。

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

在上述示例中，输入句柄是指 WDFDEVICE 对象。 此特定设备对象具有五个的子对象--两个 WDFCMRESLIST 对象、 两个 WDFCHILDLIST 对象和一个 WDFIOTARGET 对象。

 

 





