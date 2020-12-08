---
title: wdfkd.wdfusbdevice
description: Wdfkd. wdfusbdevice 扩展显示有关指定 KMDF USB 设备对象的信息，incuding 所有 USB 接口和配置的管道。
keywords:
- wdfkd wdfusbdevice Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfusbdevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e14138cb66d841dfd200f675b6aab40853a929ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823611"
---
# <a name="wdfkdwdfusbdevice"></a>!wdfkd.wdfusbdevice


！ Wdfkd; wdfusbdevice 扩展显示有关指定 Kernel-Mode Driver Framework (KMDF) USB 设备对象的信息。 此信息包括为每个接口配置的所有 USB 接口和管道。

```dbgcmd
!wdfkd.wdfusbdevice Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
WDFUSBDEVICE 类型的 USB 设备对象的句柄。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 用于修改要返回的信息类型的十六进制值。 默认值为0x0。 标志可以是以下位的任意组合：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示将包括 i/o 目标的属性。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
显示将包括每个 USB 管道对象的 i/o 目标的属性。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





