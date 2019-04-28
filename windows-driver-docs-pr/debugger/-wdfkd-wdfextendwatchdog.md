---
title: wdfkd.wdfextendwatchdog
description: Wdfkd.wdfextendwatchdog 扩展扩展了超时期限 （从 10 分钟到 24 小时） 的框架的监视程序计时器 power 转换期间。
ms.assetid: 6feb922f-0016-468c-8dd2-963db6874977
keywords:
- wdfkd.wdfextendwatchdog Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfextendwatchdog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0e1f512d9629a13f17a7daac8bd4413b6e5d4c99
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341720"
---
# <a name="wdfkdwdfextendwatchdog"></a>!wdfkd.wdfextendwatchdog


**！ Wdfkd.wdfextendwatchdog**扩展将扩展的超时期限 （从 10 分钟到 24 小时） 的框架的监视程序计时器 power 转换期间。

```dbgcmd
!wdfkd.wdfextendwatchdog Handle [Extend]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
WDFDEVICE 类型化对象的句柄。

<span id="_______Extend______"></span><span id="_______extend______"></span><span id="_______EXTEND______"></span> *扩展*   
可选。 一个值，该值指示是否启用或禁用扩展的超时期限。 如果*扩展*为 0，禁用扩展，且超时期限为 10 分钟。 如果*扩展*为 1，启用扩展，超时期限为 24 小时。 默认值为 1。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

框架的内部监视器计时器每次启动它调用的电源策略或电源事件的回调函数不是电源的驱动程序的可分页 (即，是否\_电源\_PAGABLE 位已清除)。 如果回调函数会导致分页 I/O，因此阻止操作系统系统挂起，因为没有分页设备是可用于为请求提供服务。

如果超时期限过后，框架会发出错误检查 0x10D (WDF\_冲突)。 有关详细信息，请参阅[ **Bug 检查 0x10D**](bug-check-0x10d---wdf-violation.md)。

 

 





