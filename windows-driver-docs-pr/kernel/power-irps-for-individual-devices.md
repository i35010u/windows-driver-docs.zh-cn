---
title: 单个设备的电源 IRP
description: 单个设备的电源 IRP
ms.assetid: a8d5db12-8f6b-4c65-9814-0bc3e476dd1c
keywords:
- power Irp WDK 内核设备
- 设备电源 Irp WDK 内核
- power 序列值 WDK 内核
- 工作状态返回 WDK 电源管理
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfe98ed5a1d0cbe9e5c5bf56c683259dcdf90a34
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377095"
---
# <a name="power-irps-for-individual-devices"></a>单个设备的电源 IRP





一个*设备电源 IRP*指定主要 IRP 代码[ **IRP\_MJ\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)、 一个下面列出，次要电源 IRP 代码和值**DevicePowerState**中**Power.Type**成员。

[**IRP\_MN\_查询\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)

[**IRP\_MN\_SET\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)

[**IRP\_MN\_WAIT\_WAKE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)

[**IRP\_MN\_POWER\_SEQUENCE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence)

设备堆栈中的所有驱动程序接收此类 Irp;通常情况下，仅设备电源策略管理器可以将这些 Irp 发送。 但是，电源管理器可以发送设备电源 IRP 时执行空闲检测代表一个设备，如中所述[空闲检测使用电源管理器例程](using-power-manager-routines-for-idle-detection.md)。

驱动程序将设备电源 IRP 发送任何原因如下：

-   若要查询或更改设备电源状态以响应系统电源 IRP

-   若要将处于睡眠状态，以便节约用电设备

-   若要将设备恢复为工作状态之后它一直处于睡眠状态

-   若要使设备能够唤醒以响应外部信号

-   若要启动设备时获取 power 序列值

下图显示了一系列步骤，会以发送、 转发、 完成设备电源 IRP。

![说明设备电源 irp 的路径的关系图](images/devpoirp.png)

上图所示，发送 IRP，设备电源转发，并完成以下步骤中：

1.  设备电源策略所有者调用[ **PoRequestPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)分配设备电源 IRP，并指定 PDO IRP 和回调例程 IRP 完成时要调用的目标。

2.  电源管理器分配设备电源 IRP，并将其发送到目标 PDO 设备堆栈中的顶部驱动程序。

3.  该驱动程序将执行以下操作：

    -   集[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程，如果有必要。

    -   调用[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp) （Windows Server 2003、 Windows XP 和 Windows 2000） 如果未使用完成例程。 从 Windows Vista 开始，此调用不需要且此类调用会执行任何电源管理操作。

    -   调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) （Windows 7 和 Windows Vista） 或调用[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) （Windows Server 2003、 Windows XP 和 Windows 2000) 要传递到下一步低驱动程序 IRP。

    堆栈中的每个驱动程序执行此操作直到 IRP 达到总线驱动程序。 如果驱动程序时不能 IRP，它应立即执行此操作，并调用[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)。

4.  维护设备 PDO，总线驱动程序执行请求的操作，然后调用**IoCompleteRequest**完成 IRP。 总线驱动程序可能会失败设备强化 IRP 移除某个设备或正被删除。

5.  I/O 管理器调用*IoCompletion*例程作为它们传入 IRP 设置驱动程序的向下堆栈。 毕竟*IoCompletion*已调用例程，请运行回调例程。

有关设备电源 Irp 的详细信息，请参阅[管理的电源可用于单个设备](managing-power-for-individual-devices.md)和[该有唤醒功能的支持设备](supporting-devices-that-have-wake-up-capabilities.md)。 有关 power 序列 IRP 的详细信息，请参阅[ **IRP\_MN\_POWER\_序列**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence)。

 

 




