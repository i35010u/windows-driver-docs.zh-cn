---
title: 处理等待/唤醒总线驱动程序 (PDO) 中的 IRP
description: 处理等待/唤醒总线驱动程序 (PDO) 中的 IRP
ms.assetid: 9583b935-26e1-49c6-827d-932762af114d
keywords:
- 接收等待/唤醒 Irp
- 等待/唤醒 Irp WDK 电源管理，接收
- 总线驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9185f81649a2c637aa94ce65df560c96e5673662
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519787"
---
# <a name="handling-a-waitwake-irp-in-a-bus-driver-pdo"></a>处理等待/唤醒总线驱动程序 (PDO) 中的 IRP





像其他电源 Irp，必须到总线驱动程序 (PDO)，这是最终负责完成 IRP 一直关闭设备堆栈传递每个等待/唤醒 IRP。 一旦收到 IRP，总线驱动程序可以立即失败或挂起其保存以便稍后完成。 总线驱动程序必须采取的步骤如下：

1.  检查处的值**Irp-&gt;Parameters.WaitWake.PowerState**。 如果设备支持唤醒，但不能从指定[ **SystemWake** ](systemwake.md)状态或不是从当前设备电源状态，该驱动程序应失败 IRP，如下所示：

    -   将状态设置\_无效\_设备\_状态中**Irp-&gt;IoStatus.Status**。

    -   完成 IRP ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343))，指定的 IO 优先级提升\_否\_增量。

    -   返回的状态设置**Irp-&gt;IoStatus.Status**从[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

2.  检查是否等待/唤醒 IRP 已经处于挂起状态对 PDO。 如果是这样，设置**Irp-&gt;IoStatus.Status**于状态\_设备\_繁忙、 递增的等待/唤醒 Irp，驱动程序的内部计数并完成 IRP 上, 一步中所述。

    只有一个等待/唤醒 IRP 可以处于挂起状态对 PDO。

3.  如果设备支持唤醒从指定的系统电源状态和无等待/唤醒 IRP 已挂起，请调用[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)以指示 I/O 管理器将完成 IRP 或取消更高版本。 未设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程。

4.  设置设备硬件，从而使唤醒。

    依据总线驱动程序，其硬件，唤醒是依赖于设备的特定机制。 对于 PCI 设备，Pci.sys 负责设置 PME 启用位，因为此驱动程序拥有 PME 注册。 对于其他设备，请参阅特定于设备的类的文档。

5.  如果 PDO 是子节点的 FDO[请求等待/唤醒 IRP](sending-a-wait-wake-irp.md) FDO，为确保设置[*取消*](https://msdn.microsoft.com/library/windows/hardware/ff540742)例程的当前 IRP (它包含挂起 IRP)。 不要尝试传递或重复使用当前的 IRP。

6.  返回状态\_从 PENDING *DispatchPower*例程。

7.  当唤醒信号到达时，调用**IoCompleteRequest**以完成挂起等待/唤醒 IRP，设置**Irp IoStatus.Status**到状态\_成功，并指定 IO 优先级提升\_否\_增量。

### <a name="for-devices-that-do-not-support-wake-up"></a>不支持唤醒的设备

如果设备不支持唤醒，总线驱动程序 (PDO) 时应使用，如下所示：

1.  通过调用完成等待/唤醒 IRP **IoCompleteRequest**，指定 IO\_否\_增量。

2.  返回从*DispatchPower*例程，并在将值传递**Irp-&gt;IoStatus.Status**作为其返回值。

 

 




