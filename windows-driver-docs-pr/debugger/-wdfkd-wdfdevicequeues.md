---
title: wdfkd.wdfdevicequeues
description: Wdfkd. wdfdevicequeues 扩展显示属于指定设备的所有框架队列对象的相关信息。
keywords:
- wdfkd wdfdevicequeues Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfdevicequeues
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7ad99174f9b76045e31d1ff121457f0ba435eda9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814615"
---
# <a name="wdfkdwdfdevicequeues"></a>!wdfkd.wdfdevicequeues


**！ Wdfkd wdfdevicequeues** 扩展显示属于指定设备的所有框架队列对象的相关信息。

```dbgcmd
!wdfkd.wdfdevicequeues Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
WDFDEVICE 类型化对象的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md) 和 [**！ wdfkd。 wdfqueue**](-wdfkd-wdfqueue.md)。

<a name="remarks"></a>备注
-------

下面的示例演示了 **！ wdfkd. wdfdevicequeues** 扩展中的显示。

```dbgcmd
kd> !wdfdevicequeues 0x7cad31c8 

# Dumping queues of WDFDEVICE 0x7cad31c8
=====================================
## Number of queues: 3
----------------------------------
Queue: 1 (!wdfqueue 0x7d67d1e8)
    Manual, Not power-managed, PowerOn, Can accept, Can dispatch, ExecutionLevelDispatch, SynchronizationScopeNone
    Number of driver owned requests: 0
    Number of waiting requests: 0


## This is WDF internal queue for create requests.
----------------------------------
Queue: 2 (!wdfqueue 0x7ce7d1e8)
    Parallel, Power-managed, PowerOff, Can accept, Can dispatch, ExecutionLevelDispatch, SynchronizationScopeNone
    Number of driver owned requests: 0
    Number of waiting requests: 0


##     EvtIoDefault: (0xf221fad0) wdfrawbusenumtest!EvtIoQueueDefault
----------------------------------
Queue: 3 (!wdfqueue 0x7cd671e8)
    Parallel, Power-managed, PowerOff, Can accept, Can dispatch, ExecutionLevelDispatch, SynchronizationScopeNone
    Number of driver owned requests: 0
    Number of waiting requests: 0


    EvtIoDeviceControl: (0xf2226ac0) wdfrawbusenumtest!RawBus_RawPdo_EvtDeviceControl
```

 

 





