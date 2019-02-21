---
title: wdfkd.wdfopenhandles
description: Wdfkd.wdfopenhandles 扩展显示有关指定 WDF 设备打开的所有句柄的信息。
ms.assetid: 9b62a80a-6f53-4581-98b7-8eb5f9f146c2
keywords:
- wdfkd.wdfopenhandles Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfopenhandles
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0111d4dc776e69e36ef7daf0a93b63a55acd12cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525773"
---
# <a name="wdfkdwdfopenhandles"></a>!wdfkd.wdfopenhandles


**！ Wdfkd.wdfopenhandles**扩展显示有关指定 WDF 设备打开的所有句柄的信息。

```dbgcmd
!wdfkd.wdfopenhandles Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
Framework 设备对象 (WDFDEVICE) 的句柄。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示信息的种类。 *标志*可以是以下位的任意组合。 默认值为 0x0。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示文件的对象上下文信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





