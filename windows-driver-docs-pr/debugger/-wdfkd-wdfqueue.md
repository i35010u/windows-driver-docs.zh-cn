---
title: wdfkd.wdfqueue
description: Wdfkd. wdfqueue 扩展显示有关指定框架队列对象和队列中的框架请求对象的信息。
keywords:
- wdfkd wdfqueue Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3309ce8f36625899fef348d30d85fc52b5a83faf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833715"
---
# <a name="wdfkdwdfqueue"></a>!wdfkd.wdfqueue


**！ Wdfkd wdfqueue** 扩展显示有关指定框架队列对象和队列中的框架请求对象的信息。

```dbgcmd
!wdfkd.wdfqueue Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
框架队列对象的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

下面的示例演示了 **！ wdfkd. wdfqueue** 扩展中的显示。

```dbgcmd
kd> !wdfqueue 0x7ce7d1e8 

# Dumping WDFQUEUE 0x7ce7d1e8
=========================
Parallel, Power-managed, PowerOff, Can accept, Can dispatch, ExecutionLevelDispatch, SynchronizationScopeNone
    Number of driver owned requests: 0
    Number of waiting requests: 0


    EvtIoDefault: (0xf221fad0) wdfrawbusenumtest!EvtIoQueueDefault
```

前面示例中的队列配置为进行并行调度，是电源管理的，但当前处于关闭状态，并且可以接受和调度请求。

 

 





