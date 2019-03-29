---
title: wdfkd.wdfobject
description: Wdfkd.wdfobject 扩展显示有关指定的 framework 对象的信息。
ms.assetid: fee1b924-5437-4d15-b39c-4d0f6eba0a90
keywords:
- wdfkd.wdfobject Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfobject
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 138b2a052bbc932c66eee278cb7683494cde99ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566499"
---
# <a name="wdfkdwdfobject"></a>!wdfkd.wdfobject


**！ Wdfkd.wdfobject**扩展显示有关指定的 framework 对象的信息。

```dbgcmd
!wdfkd.wdfobject FrameworkObject
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______FrameworkObject______"></span><span id="_______frameworkobject______"></span><span id="_______FRAMEWORKOBJECT______"></span> *FrameworkObject*   
指向 framework 对象的指针。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

如果驱动程序启用内核模式驱动程序框架 (KMDF) 验证器和公共的句柄类型标记为跟踪中的显示 **！ wdfkd.wdfobject**扩展包含标记跟踪器 （即，跟踪对象），在以下示例。

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

 

 





