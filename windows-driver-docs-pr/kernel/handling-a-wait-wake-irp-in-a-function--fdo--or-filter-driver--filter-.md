---
title: 处理函数 (FDO) 或筛选器驱动程序（筛选器 DO）中的等待/唤醒 IRP
description: 处理函数 (FDO) 或筛选器驱动程序（筛选器 DO）中的等待/唤醒 IRP
ms.assetid: 752b6c3c-f42a-469d-8a43-0778ecbe4541
keywords:
- 正在接收等待/唤醒 Irp
- 等待/唤醒 Irp WDK 电源管理，接收
- 函数驱动程序 WDK 电源管理
- FDOs WDK 电源管理
- 筛选 DOs WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45bfc9ca693c6139d389065a2afaafbf0ba69965
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838673"
---
# <a name="handling-a-waitwake-irp-in-a-function-fdo-or-filter-driver-filter-do"></a>处理函数 (FDO) 或筛选器驱动程序（筛选器 DO）中的等待/唤醒 IRP





当创建 FDO 或筛选器的驱动程序确实收到[**IRP\_MN\_等待**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)关联的 PDO\_唤醒请求时，它可以直接将 irp 传递到下一个较低的驱动程序，或在关闭 IRP 之前执行特定操作。

### <a name="for-devices-that-support-wake-up"></a>对于支持唤醒的设备

接收到等待/唤醒 IRP 后，函数或筛选器驱动程序应执行以下步骤：

1.  调用[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)，传递当前 IRP，以确保在处理 wait/唤醒 IRP 时，驱动程序不会收到 PnP [**IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求。

    如果[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)返回失败状态，驱动程序不应继续处理 IRP。 相反，它将完成 IRP （[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)）并返回失败状态。

2.  检查**Irp&gt;PowerState**上的值，并将[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构中的当前设备电源状态与**DeviceState**\[SystemWake\] 进行比较。

    如果设备支持唤醒，但不支持从指定的[SystemWake](systemwake.md)状态进行唤醒，或者不是从当前设备电源状态进行的，则该驱动程序应使 IRP 失败，如下所示：

    -   设置状态\_无效\_设备\_Irp 中**的状态-&gt;IoStatus**。
    -   完成 IRP （**IoCompleteRequest**），指定 IO\_NO\_递增的优先级提升。
    -   返回[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中的**Irp&gt;IoStatus**的状态集。

3.  否则，请使用[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)为 IRP 设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程。 *IoCompletion*例程应执行驱动程序将设备返回到工作状态所需的任何任务。

    如果已取消 IRP，还将调用*IoCompletion*例程。

4.  保存驱动程序在其*IoCompletion*例程中可能需要的所有信息。

5.  调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) （在 windows 7 和 windows Vista 中）或[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) （在 Windows SERVER 003、windows XP 和 windows 2000 中），将 wait/唤醒 IRP 传递到下一个较低版本的驱动程序。

6.  调用[**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)以释放以前获取的锁。

7.  [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程返回状态\_挂起。 驱动程序在保存 IRP 时，不得更改**irp&gt;IoStatus**中的值。

### <a name="for-devices-that-do-not-support-wake-up"></a>对于不支持唤醒的设备

如果函数或筛选器驱动程序接收到不支持唤醒功能的设备的等待/唤醒 IRP，则该驱动程序应该会使 IRP 失败，如下所示：

1.  完成 IRP （**IoCompleteRequest**），指定 IO\_NO\_递增的优先级提升。

2.  返回[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中的**Irp&gt;IoStatus**的状态集。

 

 




