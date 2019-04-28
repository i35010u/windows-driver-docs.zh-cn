---
title: wdfkd.wdfdevicequeues
description: Wdfkd.wdfdevicequeues 扩展显示的所有框架队列对象属于指定设备有关的信息。
ms.assetid: bd0e7fcc-b561-48fb-901a-605e9d647b61
keywords:
- wdfkd.wdfdevicequeues Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfdevicequeues
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d46ae2fe52473f64845d16191813a91c62e35fff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341758"
---
# <a name="wdfkdwdfdevicequeues"></a>!wdfkd.wdfdevicequeues


**！ Wdfkd.wdfdevicequeues**扩展显示的所有框架队列对象属于指定设备有关的信息。

```dbgcmd
!wdfkd.wdfdevicequeues Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
WDFDEVICE 类型化对象的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)并[ **！ wdfkd.wdfqueue**](-wdfkd-wdfqueue.md)。

<a name="remarks"></a>备注
-------

下面的示例演示从显示 **！ wdfkd.wdfdevicequeues**扩展。

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

 

 





