---
title: wudfext.wudfdevice
description: Wudfext.wudfdevice 扩展显示插即用 (PnP) 和设备的电源管理状态系统。
ms.assetid: d070f5ba-97c0-47f8-869f-54a3d3395476
keywords:
- wudfext.wudfdevice Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfdevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 169d998f46d00cb2b31e36d3c05aacc43d9ff88f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533750"
---
# <a name="wudfextwudfdevice"></a>!wudfext.wudfdevice


**！ Wudfext.wudfdevice**扩展显示插即用 (PnP) 和设备的电源管理状态系统。

```dbgcmd
!wudfext.wudfdevice pWDFDevice
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______pWDFDevice______"></span><span id="_______pwdfdevice______"></span><span id="_______PWDFDEVICE______"></span> *pWDFDevice*   
指定的地址**IWDFDevice**界面来显示有关即插即用或电源管理状态。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

可以使用 **！ wudfext.wudfdevice**扩展来确定的设备的即插即用或电源管理状态的*pWDFDevice*参数指定。

以下是一种 **！ wudfext.wudfdevice**显示：

```dbgcmd
kd> !wudfdevice 0xf2f80 
Pnp Driver Callbacks:
  IPnpCallback: 0x0
  IPnpCallbackHardware: 0x0
  IPnpSelfManagedIo: 0x0
Pnp State Machine:
  CurrentState:  WdfDevStatePnpStarted
  Pending UMIrp: 0x00000000
    Could not read event queue depth, assuming 8
  Event queue:
    Processed/in-process events:
      PnpEventAddDevice
      PnpEventStartDevice
      PnpEventPwrPolStarted
    Pending events:
    State History:
      WdfDevStatePnpInit
      WdfDevStatePnpInitStarting
      WdfDevStatePnpHardwareAvailable
      WdfDevStatePnpEnableInterfaces
      WdfDevStatePnpStarted
Power State Machine:
  CurrentState:      WdfDevStatePowerD0
  Pending UMIrp:     0x00000000
  IoCallbackFailure: false
    Could not read event queue depth, assuming 8
  Event queue:
    Processed/in-process events:
      PowerImplicitD0
    Pending events:
    State History:
      WdfDevStatePowerStartingCheckDeviceType
      WdfDevStatePowerD0Starting
      WdfDevStatePowerD0StartingConnectInterrupt
      WdfDevStatePowerD0StartingDmaEnable
      WdfDevStatePowerD0StartingStartSelfManagedIo
      WdfDevStatePowerDecideD0State
      WdfDevStatePowerD0
Power Policy State Machine:
  CurrentState             : WdfDevStatePwrPolStartingSucceeded
  PowerPolicyOwner         : false
  PendingSystemPower UMIrp : 0x00000000
  PowerFailed              : false
    Could not read event queue depth, assuming 8
  Event queue:
    Processed/in-process events:
      PwrPolStart
      PwrPolPowerUp
    Pending events:
    State History:
      WdfDevStatePwrPolStarting
      WdfDevStatePwrPolStarted
      WdfDevStatePwrPolStartingSucceeded
```

 

 





