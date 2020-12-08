---
title: wdfkd.wdfdevice
description: Wdfkd. wdfdevice 扩展显示与 WDFDEVICE 类型的对象句柄关联的信息。
keywords:
- wdfkd wdfdevice Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfdevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d369a75d6117c00a7b6bd52af335e113d6b9e46f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814617"
---
# <a name="wdfkdwdfdevice"></a>!wdfkd.wdfdevice


**！ Wdfkd wdfdevice** 扩展显示与 wdfdevice 类型的对象句柄关联的信息。

```dbgcmd
!wdfkd.wdfdevice Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
WDFDEVICE 类型化对象的句柄。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 要显示的信息的类型。 *标志* 可以是以下位的任意组合：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
此显示内容将包含有关设备的详细信息，例如，关联的 WDFCHILDLIST 类型的句柄、同步范围和执行级别。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
显示内容将包括详细的电源状态信息。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
显示内容将包括详细的电源策略状态信息。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>第 3 (0x8)   
显示内容将包括详细即插即用 (PnP) 状态信息。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)   
显示将包括设备对象的回调函数。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

下面的示例在 wdfkd PDO)  (PDO 的 WDFDEVICE 句柄上使用 **！ wdfdevice** 扩展，无需指定任何标志。

```dbgcmd
kd> !wdfdevice 0x7cad31c8 

# Dumping WDFDEVICE 0x7cad31c8
=================================

WDM PDEVICE_OBJECTs:  self 81fb00e8

Pnp state:  119 ( WdfDevStatePnpStarted )
Power state:  31f ( WdfDevStatePowerDx )
Power Pol state:  508 ( WdfDevStatePwrPolWaitingUnarmed )

Parent WDFDEVICE 7ca7b1c0
Parent states:
   Pnp state:  119 ( WdfDevStatePnpStarted )
   Power state:  307 ( WdfDevStatePowerD0 )
   Power Pol state:  565 ( WdfDevStatePwrPolStarted )

No pended pnp or power irps
Device is the power policy owner for the stack
```

下面的示例显示与前面的示例相同的设备对象，但此时间的标志值为0xF。 此标志值（位0x1、0x2、0x4 和0x8 的组合）将导致显示内容包括详细设备信息、电源状态信息、电源策略状态信息和 PnP 状态信息。

```dbgcmd
kd> !wdfdevice 0x7cad31c8 f 

# Dumping WDFDEVICE 0x7cad31c8
=================================

WDM PDEVICE_OBJECTs:  self 81fb00e8

Pnp state:  119 ( WdfDevStatePnpStarted )
Power state:  31f ( WdfDevStatePowerDx )
Power Pol state:  508 ( WdfDevStatePwrPolWaitingUnarmed )

Parent WDFDEVICE 7ca7b1c0
Parent states:
   Pnp state:  119 ( WdfDevStatePnpStarted )
   Power state:  307 ( WdfDevStatePowerD0 )
   Power Pol state:  565 ( WdfDevStatePwrPolStarted )

No pended pnp or power irps
Device is the power policy owner for the stack

Pnp state history:
[0] WdfDevStatePnpObjectCreated (0x100)
[1] WdfDevStatePnpInit (0x105)
[2] WdfDevStatePnpInitStarting (0x106)
[3] WdfDevStatePnpHardwareAvailable (0x108)
[4] WdfDevStatePnpEnableInterfaces (0x109)
[5] WdfDevStatePnpStarted (0x119)

Power state history:
[0] WdfDevStatePowerD0StartingConnectInterrupt (0x310)
[1] WdfDevStatePowerD0StartingDmaEnable (0x311)
[2] WdfDevStatePowerD0StartingStartSelfManagedIo (0x312)
[3] WdfDevStatePowerDecideD0State (0x313)
[4] WdfDevStatePowerD0BusWakeOwner (0x309)
[5] WdfDevStatePowerGotoDx (0x31a)
[6] WdfDevStatePowerGotoDxIoStopped (0x31c)
[7] WdfDevStatePowerDx (0x31f)

Power policy state history:
[0] WdfDevStatePwrPolStarting (0x501)
[1] WdfDevStatePwrPolStartingSucceeded (0x502)
[2] WdfDevStatePwrPolStartingDecideS0Wake (0x504)
[3] WdfDevStatePwrPolStartedIdleCapable (0x505)
[4] WdfDevStatePwrPolTimerExpiredNoWake (0x506)
[5] WdfDevStatePwrPolTimerExpiredNoWakeCompletePowerDown (0x507)
[6] WdfDevStatePwrPolWaitingUnarmedQueryIdle (0x509)
[7] WdfDevStatePwrPolWaitingUnarmed (0x508)

WDFCHILDLIST Handles:
 !WDFCHILDLIST 0x7ce710c8

SyncronizationScope is WdfSynchronizationScopeNone
ExecutionLevel is WdfExecutionLevelDispatch
```

 

 





