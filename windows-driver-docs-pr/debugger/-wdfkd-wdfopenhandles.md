---
title: wdfkd.wdfopenhandles
description: Wdfkd. wdfopenhandles 扩展显示有关在指定的 WDF 设备上打开的所有句柄的信息。
keywords:
- wdfkd wdfopenhandles Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfopenhandles
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1a6e8a24a8a75038cc7e04a628305b809818e399
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795699"
---
# <a name="wdfkdwdfopenhandles"></a>!wdfkd.wdfopenhandles


**！ Wdfkd wdfopenhandles** 扩展显示有关在指定的 WDF 设备上打开的所有句柄的信息。

```dbgcmd
!wdfkd.wdfopenhandles Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
 (WDFDEVICE) 的框架设备对象的句柄。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 指定要显示的信息的类型。 *标志* 可以是以下位的任意组合。 默认值为0x0。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示文件对象上下文信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





