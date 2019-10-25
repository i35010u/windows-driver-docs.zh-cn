---
title: 取消等待/唤醒 IRP
description: 取消等待/唤醒 IRP
ms.assetid: 08e1d11a-91a3-496a-b3ad-f99456e4ce1d
keywords:
- 电源管理 WDK 内核，唤醒功能
- 外部唤醒信号 WDK
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
- IRP_MN_WAIT_WAKE
- 等待/唤醒 Irp WDK 电源管理，取消
- 正在取消等待/唤醒 Irp
- 取消例程，等待/唤醒 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: eabf931baf7b34d4a082c0477c6e8c4116341558
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828549"
---
# <a name="canceling-a-waitwake-irp"></a>取消等待/唤醒 IRP





只有发送等待/唤醒 IRP 的驱动程序才能取消该 IRP。

在以下情况下，驱动程序可能需要取消挂起的等待/唤醒 IRP：

-   驱动程序接收 PnP [**IRP\_MN\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)， [**IRP\_MN\_查询\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)， [**IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)，或[**IRP\_MN\_对设备的意外\_删除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)请求。 设备重新启动后，驱动程序应重新发出等待/唤醒 IRP （[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)）。

-   系统将进入睡眠状态，但不应启用设备来唤醒系统。

    例如，USB 集线器驱动程序可能会在设备启动时发送**IRP\_MN\_等待\_唤醒**请求，以防稍后将其输入设备之一置于睡眠状态。 当系统处于工作状态时，来自设备的唤醒信号会将设备返回到工作状态（但不会影响系统电源状态）。 当系统准备关闭时，如果不应允许设备唤醒系统，则 USB 集线器驱动程序会取消此 IRP。

-   系统正在进入睡眠状态，设备无法唤醒该状态。 也就是说，它所输入的状态比[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构中指定的[**SystemWake**](systemwake.md)值更少。

-   设备进入电源状态，它无法响应唤醒信号。 也就是说，它所输入的状态小于其**设备\_功能**结构中指定的[**DeviceWake**](devicewake.md)值。

若要取消等待/唤醒 IRP，发送 IRP 的驱动程序将调用[**IoCancelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)，并将指针传递到以前在驱动程序调用**PoRequestPowerIrp**时返回的 IRP。

驱动程序不得取消未发送的等待/唤醒 IRP。

### <a href="" id="ddk-cancel-routines-for-wait-wake-irps-kg"></a>等待/唤醒 Irp 的取消例程

许多函数和总线驱动程序应为挂起的等待/唤醒 Irp 设置[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程;以下类型的驱动程序必须设置此类例程：

-   将设备设置更改为启用或禁用唤醒的驱动程序。

-   发送[**IRP\_MN\_等待\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)对父设备驱动程序的唤醒请求的驱动程序。

通过[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程，驱动程序可以对其设备禁用唤醒功能，并清除与挂起的等待/唤醒 IRP 相关的任何数据。 为父设备请求等待/唤醒 Irp 的驱动程序也可以取消这些 Irp。

在其等待/唤醒*取消*例程中，驱动程序应执行以下步骤：

1.  调用[**IoSetCancelRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)将 IRP 的*取消*例程重置为**NULL**。

2.  调用[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))，传递 irp 中指定的**irp->cancelirql** ，以释放 irp 的取消旋转锁。

3.  重置设备扩展中的所有相关字段。 例如，等待/唤醒 IRP 处于挂起状态时，大多数驱动程序会设置一个标志，并在设备扩展中保留一个指向 IRP 的指针。

    请注意，驱动程序可以在取消其他此类 IRP 时接收等待/唤醒 IRP。 驱动程序必须检查它是否已在旋转锁定保护（或其等效项）下具有 IRP。 如果是这样，则驱动程序必须仔细同步其处理，以确保它取消了正确的 IRP。 有关在*取消*例程中使用自旋锁的详细信息，请参阅[取消 irp](canceling-irps.md)。

4.  更改任何所需的设备设置。 例如，调制解调器驱动程序将禁用设备的唤醒设置。

5.  将**Irp&gt;IoStatus**设置为状态\_取消。

6.  调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)完成等待/唤醒 IRP，指定 IO\_没有\_增量。

7.  如果驱动程序以前请求相关的**IRP\_MN\_等待父设备\_唤醒**，则驱动程序应在其*取消*例程内取消该 irp。 驱动程序必须先释放 cancel 自旋锁，然后才能取消父级的 IRP。

    例如，作为设备的总线驱动程序并拥有其父项的电源策略驱动程序的驱动程序应取消其之前发送到其父项的相关等待/唤醒 IRP。 调用[**IoCancelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)将调用父级的*Cancel*例程，并沿设备堆栈向下。

 

 




