---
title: wdfkd.wdfqueue
description: Wdfkd.wdfqueue 扩展显示有关指定的框架队列对象和在队列中的框架请求对象的信息。
ms.assetid: 100917dc-9ce9-48d6-a285-58ea78a4c2f4
keywords:
- wdfkd.wdfqueue Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5e1d481c4c9efa1ae1017d601c3d14c8d635a9be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540949"
---
# <a name="wdfkdwdfqueue"></a>!wdfkd.wdfqueue


**！ Wdfkd.wdfqueue**扩展显示有关指定的框架队列对象和在队列中的框架请求对象的信息。

```dbgcmd
!wdfkd.wdfqueue Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
Framework 队列对象的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

下面的示例演示从显示 **！ wdfkd.wdfqueue**扩展。

```dbgcmd
kd> !wdfqueue 0x7ce7d1e8 

# Dumping WDFQUEUE 0x7ce7d1e8
=========================
Parallel, Power-managed, PowerOff, Can accept, Can dispatch, ExecutionLevelDispatch, SynchronizationScopeNone
    Number of driver owned requests: 0
    Number of waiting requests: 0


    EvtIoDefault: (0xf221fad0) wdfrawbusenumtest!EvtIoQueueDefault
```

前面的示例中的队列配置为并行调度，是电源管理，但当前处于关闭状态，并可以同时接受和调度请求。

 

 





