---
title: wdfkd.wdfdmaenablers
description: Wdfdmaenablers 扩展显示 (DMA) 与指定设备对象相关联的对象的所有 WDF 直接内存访问。
keywords:
- wdfkd wdfdmaenablers Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfdmaenablers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b1fed11542a766e363281bbd67489a65d59f9cf6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822635"
---
# <a name="wdfkdwdfdmaenablers"></a>!wdfkd.wdfdmaenablers


**！ Wdfkd wdfdmaenablers** 扩展显示 (DMA) 与指定设备对象相关联的对象的所有 WDF 直接内存访问。 它还显示其关联的事务和公用缓冲区对象。

```dbgcmd
!wdfkd.wdfdmaenablers Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
 (WDFDEVICE) 的框架设备对象的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





