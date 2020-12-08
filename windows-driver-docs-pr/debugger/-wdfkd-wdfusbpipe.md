---
title: wdfkd.wdfusbpipe
description: Wdfkd wdfusbpipe 扩展显示 Kernel-Mode Driver Framework (KMDF) USB 管道对象的 i/o 目标的信息。
keywords:
- wdfkd wdfusbpipe Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfusbpipe
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0f018bd88e93e5ef9844d73da2609215983f35b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823597"
---
# <a name="wdfkdwdfusbpipe"></a>!wdfkd.wdfusbpipe


**！ Wdfkd wdfusbpipe** 扩展显示 Kernel-Mode Driver FRAMEWORK (KMDF) USB 管道对象的 i/o 目标的信息。

```dbgcmd
!wdfkd.wdfusbpipe Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
WDFUSBPIPE 类型的 USB 管道对象的句柄。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 用于修改要返回的信息类型的十六进制值。 默认值为0x0。 标志可以是以下位的任意组合：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示将包括 i/o 目标的属性。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





