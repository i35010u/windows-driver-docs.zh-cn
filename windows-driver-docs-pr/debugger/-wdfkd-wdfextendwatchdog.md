---
title: wdfkd.wdfextendwatchdog
description: Wdfextendwatchdog 扩展将 (在电源转换期间从10分钟到24小时) 的超时时间。
keywords:
- wdfkd wdfextendwatchdog Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfextendwatchdog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1e5d43d04500de0317ce496e320747216f064318
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839331"
---
# <a name="wdfkdwdfextendwatchdog"></a>!wdfkd.wdfextendwatchdog


**！ Wdfkd wdfextendwatchdog** 扩展将 (从10分钟到24小时之间的超时时间) 扩展到电源转换期间框架的监视程序计时器。

```dbgcmd
!wdfkd.wdfextendwatchdog Handle [Extend]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
WDFDEVICE 类型化对象的句柄。

<span id="_______Extend______"></span><span id="_______extend______"></span><span id="_______EXTEND______"></span>*扩展*   
可选。 一个值，该值指示是启用还是禁用超时期限的扩展。 如果 *扩展* 为0，则禁用扩展，并且超时期限为10分钟。 如果 *扩展* 为1，则启用扩展，并且超时期限为24小时。 默认值为 1。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

框架在每次为不能使用 power 可分页的驱动程序调用电源策略或电源事件回调函数时都启动一个内部监视程序计时器 (也就是说，"DO \_ power \_ PAGABLE" 位是) 的。 如果回调函数导致分页 i/o 导致阻塞，则操作系统会挂起，因为没有寻呼设备可用于处理请求。

如果超时时间已过，则框架将发出 bug 检查 0x10D (WDF \_ 冲突) 。 有关详细信息，请参阅 [**Bug 检查 0x10D**](bug-check-0x10d---wdf-violation.md)。

 

 





