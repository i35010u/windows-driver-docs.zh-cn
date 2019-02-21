---
title: wdfkd.wdfdmaenablers
description: Wdfkd.wdfdmaenablers 扩展显示与指定的设备对象相关联的所有 WDF 直接内存访问 (DMA) 对象。
ms.assetid: 31b185e7-74d3-4329-b389-37279e5aa75c
keywords:
- wdfkd.wdfdmaenablers Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfdmaenablers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e021324d3d2ea7cc911331e73124920d9c57bfae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542781"
---
# <a name="wdfkdwdfdmaenablers"></a>!wdfkd.wdfdmaenablers


**！ Wdfkd.wdfdmaenablers**扩展插件都会显示与指定的设备对象关联的所有 WDF 直接内存访问 (DMA) 对象。 它还显示其关联的事务和公共缓冲区对象。

```dbgcmd
!wdfkd.wdfdmaenablers Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
Framework 设备对象 (WDFDEVICE) 的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





