---
title: wdfkd.wdfspinlock
description: Wdfkd. wdfspinlock 扩展显示有关框架旋转锁定对象的信息。 此信息包括自旋锁的获取历史记录以及持有锁的时间长度。
keywords:
- wdfkd wdfspinlock Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfspinlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d79428d194b3961078e0f165ef45cc08ac738d12
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785305"
---
# <a name="wdfkdwdfspinlock"></a>!wdfkd.wdfspinlock


**！ Wdfkd wdfspinlock** 扩展显示有关框架旋转锁定对象的信息。 此信息包括自旋锁的获取历史记录以及持有锁的时间长度。

```dbgcmd
!wdfkd.wdfspinlock Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
WDFSPINLOCK 类型化对象的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





