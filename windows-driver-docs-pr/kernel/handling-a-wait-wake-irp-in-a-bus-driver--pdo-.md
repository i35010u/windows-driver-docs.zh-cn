---
title: 处理总线驱动程序 (PDO) 中的等待/唤醒 IRP
description: 处理总线驱动程序 (PDO) 中的等待/唤醒 IRP
keywords:
- 正在接收等待/唤醒 Irp
- 等待/唤醒 Irp WDK 电源管理，接收
- 总线驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae99adc360f213e3eb74b487d4a94a75dccf9f77
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825125"
---
# <a name="handling-a-waitwake-irp-in-a-bus-driver-pdo"></a>处理总线驱动程序 (PDO) 中的等待/唤醒 IRP





与其他电源 Irp 一样，每个等待/唤醒 IRP 都必须按设备堆栈向下传递到总线驱动程序， (PDO) ，最终负责完成 IRP。 在收到 IRP 后，总线驱动程序可以立即将其故障转移，或将其挂起以等待以后完成。 以下是总线驱动程序必须执行的步骤：

1.  检查 **Irp- &gt; WaitWake. PowerState** 的值。 如果设备支持唤醒，但不支持从指定的 [**SystemWake**](systemwake.md) 状态进行唤醒，或者不是从当前设备电源状态进行的，则该驱动程序应使 IRP 失败，如下所示：

    -   设置状态 \_ 无效的 \_ 设备 \_ 状态 **- &gt; IoStatus。状态**。

    -   完成 IRP ([**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) ，同时指定 IO 无增量的优先级 \_ 提升 \_ 。

    -   返回 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程的 **&gt; IoStatus** 中设置的状态。

2.  检查是否已为 PDO 等待等待/唤醒 IRP。 如果是这样，请将 **Irp- &gt; IoStatus** 设置为状态 \_ 设备 \_ 忙，增加驱动程序的等待/唤醒 irp 的内部计数，并按上一步所述完成 Irp。

    PDO 只能挂起一个等待/唤醒 IRP。

3.  如果设备支持从指定的系统电源状态唤醒，并且没有等待/唤醒 IRP 处于挂起状态，则调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 向 i/o 管理器指示 IRP 将在以后完成或取消。 不要设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。

4.  将设备硬件设置为启用唤醒。

    总线驱动程序使其硬件可用于唤醒的特定机制与设备相关。 对于 PCI 设备，Pci.sys 负责设置 PME-启用位，因为此驱动程序拥有 PME 寄存器。 对于其他设备，请参阅特定于设备的文档。

5.  如果 PDO 是 FDO 的子，请为 FDO [请求等待/唤醒 IRP](sending-a-wait-wake-irp.md) ，并确保为当前 irp 设置 " [*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) " 例程，使其) 挂起的 irp (。 不要尝试传递或重新使用当前 IRP。

6.  \_从 *DispatchPower* 例程返回的状态为 "挂起"。

7.  唤醒信号到达后，调用 **IoCompleteRequest** 以完成挂起的等待/唤醒 IRP，将 **IRP-IOSTATUS** 设置为状态 \_ "成功"，并指定 IO 的优先级提升 \_ 无 \_ 增量。

### <a name="for-devices-that-do-not-support-wake-up"></a>对于不支持 Wake-Up 的设备

如果设备不支持唤醒，则总线驱动程序 (PDO) 应按照以下步骤进行操作：

1.  通过调用 **IoCompleteRequest** 来完成 wait/唤醒 IRP，同时指定 IO \_ 无 \_ 增量。

2.  从 *DispatchPower* 例程返回，并将 **&gt; IoStatus** 的值作为其返回值传递。

 

