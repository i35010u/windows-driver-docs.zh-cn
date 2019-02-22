---
title: 在响应系统集 Power IRP 发送设备集 Power IRP
description: 在响应系统集 Power IRP 发送设备集 Power IRP
ms.assetid: b2029292-d770-4095-8bd7-9358b282216c
keywords:
- 发送集 power Irp
- 设置 power Irp WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a9b96219bd9ced1b5761dda271fb261388a2126
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522904"
---
# <a name="sending-a-device-set-power-irp-in-response-to-a-system-set-power-irp"></a>在响应系统集 Power IRP 发送设备集 Power IRP





设备电源策略所有者应执行以下步骤来响应系统集 power IRP:

1.  调用[ **IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)，将为当前的 IRP 传递*标记*参数，以确保该驱动程序不接收插[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)请求，而同时处理 IRP 的能力。

    如果**IoAcquireRemoveLock**返回失败状态，该驱动程序不应继续处理 IRP。 相反，从 Windows Vista 开始，驱动程序应调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)来完成请求，并返回故障状态。 在 Windows Server 2003、 Windows XP 和 Windows 2000 中，该驱动程序首先应调用[ **PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776)，调用**IoCompleteRequest**完成 IRP，，然后返回故障状态。

2.  通过调用设置下一步低驱动程序的 IRP 堆栈位置[ **IoCopyCurrentIrpStackLocationToNext**](https://msdn.microsoft.com/library/windows/hardware/ff548387)。

3.  设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例行系统中设置 power IRP。

4.  调用[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)标记系统集 power IRP 为挂起。

5.  调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336) （从 Windows Vista 开始） 或[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) （在 Windows Server 2003、 Windows XP 和 Windows 2000） 到系统将传递到下一步低驱动程序集 power IRP。

6.  返回状态\_PENDING 从其[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

在中*IoCompletion*例程 （请参阅上面的列表中第 3 步），设备电源策略所有者发送设备集 power IRP，如下所示：

1.  检查系统集 power IRP，若要获取请求的系统电源状态。 选择该系统电源状态的适当的设备电源状态。 有关详细信息，请参阅[确定正确设备电源状态](determining-the-correct-device-power-state.md)。

2.  调用[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)发送[ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)为在步骤 1 中确定设备电源状态。 电源策略所有者必须发送的设备集 power 请求，即使设备已处于该状态。

3.  指定电源完成回调例程 (*CompletionFunction*) 在调用**PoRequestPowerIrp** ，并将传递系统中的设置 power IRP*上下文*缓冲区。

4.  返回状态\_更多\_处理\_需*IoCompletion*例程，从而使该驱动程序可以结束处理系统集 power IRP power 完成回调例程中的。

请记住，不仅设备电源策略所有者将发送的设备集 power IRP，但还必须处理此 IRP，传输时通过设备堆栈。 因此，设备电源策略所有者可能不只与设备关联的 power 完成回调例程集 power IRP 和一个*IoCompletion*例行系统集 power IRP，而且还*IoCompletion*例程设备集 power IRP。 有关详细信息，请参阅[处理 IRP\_MN\_设置\_的电源可用于设备的电源状态](handling-irp-mn-set-power-for-device-power-states.md)。

后 I/O 管理器调用所有*IoCompletion*已设置为设备向设备堆栈下的行程集 power IRP 的例程，I/O 管理器调用 power 完成回调例程。 此时，堆栈中的所有驱动程序已完成设备设置 power IRP 和设备电源转换已完成。

Power 完成回调例程必须执行以下操作：

1.  调用[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)启动下一个幂 IRP。 （Windows Server 2003、 Windows XP 和 Windows 2000 仅。）

2.  完成系统集 power IRP ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)) 与返回设备的状态集 power IRP。

3.  调用[ **IoReleaseRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549560)来释放以前获取的锁。

4.  返回与集 power Irp 已完成的状态。

 

 




