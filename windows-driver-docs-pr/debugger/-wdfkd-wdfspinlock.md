---
title: wdfkd.wdfspinlock
description: Wdfkd.wdfspinlock 扩展显示有关 framework 自旋锁对象的信息。 此信息包括旋转锁获取历史记录和在持有锁定时的时间长度。
ms.assetid: 73e74703-ed9b-460b-a798-41bb56942aa3
keywords:
- wdfkd.wdfspinlock Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfspinlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4f59ac337b4d830e36b8585afed03e343d23c005
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323177"
---
# <a name="wdfkdwdfspinlock"></a>!wdfkd.wdfspinlock


**！ Wdfkd.wdfspinlock**扩展显示有关 framework 自旋锁对象的信息。 此信息包括旋转锁获取历史记录和在持有锁定时的时间长度。

```dbgcmd
!wdfkd.wdfspinlock Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
WDFSPINLOCK 类型化对象的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





