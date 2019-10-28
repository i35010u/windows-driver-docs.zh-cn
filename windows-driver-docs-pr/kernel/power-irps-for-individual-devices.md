---
title: 单个设备的电源 IRP
description: 单个设备的电源 IRP
ms.assetid: a8d5db12-8f6b-4c65-9814-0bc3e476dd1c
keywords:
- power Irp WDK 内核，设备
- 设备电源 Irp WDK 内核
- 幂序列值 WDK 内核
- 工作状态返回 WDK 电源管理
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2064f6f032e0fca0c9a2008275f18e0076b4874
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838502"
---
# <a name="power-irps-for-individual-devices"></a>单个设备的电源 IRP





*设备电源 IRP*指定\_MJ 的主要 Irp 代码[**irp\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)、下面列出的其中一个小电源 IRP 代码，以及**DevicePowerState**成员中的值 **。**

[**IRP\_MN\_QUERY\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)

[**IRP\_MN\_集\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)

[**IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)

[**IRP\_MN\_电源\_序列**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence)

设备堆栈中的所有驱动程序都接收此类 Irp;通常，只有设备电源策略管理器可以发送这些 Irp。 但是，在代表设备执行空闲检测时，电源管理器可以发送设备电源 IRP，如[使用电源管理器例程进行空闲检测](using-power-manager-routines-for-idle-detection.md)中所述。

驱动程序出于以下任何原因发送设备电源 IRP：

-   查询或更改设备电源状态以响应系统电源 IRP

-   使设备进入睡眠状态以节省电源

-   使设备在睡眠后返回到工作状态

-   允许设备唤醒以响应外部信号

-   在打开设备时获取电源序列值

下图显示了发送、转发和完成设备电源 IRP 的步骤顺序。

![说明设备电源 irp 路径的示意图](images/devpoirp.png)

如上图所示，将在以下步骤中发送、转发和完成设备电源 IRP：

1.  设备电源策略所有者调用[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)来分配设备电源 IRP，并指定作为 irp 目标的 PDO 和 irp 完成时要调用的回调例程。

2.  对于目标 PDO，电源管理器会分配设备电源 IRP，并将其发送到设备堆栈中的顶层驱动程序。

3.  驱动程序执行以下操作：

    -   设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程（如果需要）。

    -   如果未使用完成例程，则调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) （windows Server 2003、windows XP 和 windows 2000）。 从 Windows Vista 开始，此调用不是必需的，因此，这种调用不会执行任何电源管理操作。

    -   调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) （windows 7 和 windows Vista）或调用[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) （Windows SERVER 2003、windows XP 和 windows 2000），将 IRP 向下传递到下一个较低版本的驱动程序。

    堆栈中的每个驱动程序都将执行此项，直到 IRP 到达总线驱动程序。 如果某个驱动程序必须失败 IRP，它应立即执行此操作，并调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)。

4.  总线驱动程序（用于维护设备 PDO）执行请求的操作，然后调用**IoCompleteRequest**来完成 IRP。 如果设备被删除或已被删除，则总线驱动程序可以使设备开启 IRP 失败。

5.  当驱动程序通过将 IRP 向下传递到堆栈中时，i/o 管理器将调用由驱动程序设置的*IoCompletion*例程。 调用完所有*IoCompletion*例程后，将运行回调例程。

有关设备电源 Irp 的详细信息，请参阅[管理单个设备的电源](managing-power-for-individual-devices.md)和[具有唤醒功能的支持设备](supporting-devices-that-have-wake-up-capabilities.md)。 有关电源序列 IRP 的详细信息，请参阅[**IRP\_MN\_power\_序列**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence)。

 

 




