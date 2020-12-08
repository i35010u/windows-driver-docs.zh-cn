---
title: wdfkd.wdfusbinterface
description: Wdfkd wdfusbinterface 扩展显示有关指定 Kernel-Mode Driver Framework (KMDF) USB 接口对象的信息，其中包括可能的设置和当前设置。
keywords:
- wdfkd wdfusbinterface Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfusbinterface
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ff800c70b59af86e1ff310b0b0f4c49bfac75fe9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823609"
---
# <a name="wdfkdwdfusbinterface"></a>!wdfkd.wdfusbinterface


**！ Wdfkd wdfusbinterface** 扩展显示有关指定 Kernel-Mode Driver FRAMEWORK (KMDF) USB 接口对象的信息，其中包括可能的设置和当前设置。

```dbgcmd
!wdfkd.wdfusbinterface Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
WDFUSBINTERFACE 类型的 USB 接口对象的句柄。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 用于修改要返回的信息类型的十六进制值。 默认值为0x0。 标志可以是以下位的任意组合：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示将包括每个 KMDF USB 管道对象的 i/o 目标的属性。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





