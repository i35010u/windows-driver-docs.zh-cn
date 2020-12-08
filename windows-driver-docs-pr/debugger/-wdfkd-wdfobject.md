---
title: wdfkd.wdfobject
description: Wdfkd. wdfobject 扩展显示有关指定框架对象的信息。
keywords:
- wdfkd wdfobject Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfobject
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 95643ee69a9c3e625965436237104e2ea68a3de5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795703"
---
# <a name="wdfkdwdfobject"></a>!wdfkd.wdfobject


**！ Wdfkd wdfobject** 扩展显示有关指定框架对象的信息。

```dbgcmd
!wdfkd.wdfobject FrameworkObject
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______FrameworkObject______"></span><span id="_______frameworkobject______"></span><span id="_______FRAMEWORKOBJECT______"></span>*FrameworkObject*   
指向框架对象的指针。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

如果为驱动程序启用了 Kernel-Mode Driver Framework (KMDF) 验证程序，并且公用句柄类型已标记为要跟踪，则从 **！ wdfkd wdfobject** 扩展中的显示包括标记跟踪器 (，即跟踪对象) ，如以下示例中所示。

```dbgcmd
kd> !wdfobject 0x83584e38 

The type for object 0x83584e38 is FxDevice
State: FxObjectStateCreated (0x1)

!wdfhandle 0x7ca7b1c0

dt FxDevice 0x83584e38

    context:  dt 0x83584ff8 ROOT_CONTEXT (size is 0x1 bytes)
     <no associated attribute callbacks>

Object debug extension 83584e20
   !wdftagtracker 0x83722d80
   Verifier lock 0x831cefa8

   State history:
    [0] FxObjectStateCreated (0x1)
```

 

 





