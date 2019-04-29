---
title: 处理函数 (FDO) 或筛选器驱动程序（筛选器 DO）中的等待/唤醒 IRP
description: 处理函数 (FDO) 或筛选器驱动程序（筛选器 DO）中的等待/唤醒 IRP
ms.assetid: 752b6c3c-f42a-469d-8a43-0778ecbe4541
keywords:
- 接收等待/唤醒 Irp
- 等待/唤醒 Irp WDK 电源管理，接收
- 功能的驱动程序 WDK 电源管理
- FDOs WDK 电源管理
- 筛选器 DOs WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c88994c9d124c8decbe07e6f92729791c6337de9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359819"
---
# <a name="handling-a-waitwake-irp-in-a-function-fdo-or-filter-driver-filter-do"></a>处理函数 (FDO) 或筛选器驱动程序（筛选器 DO）中的等待/唤醒 IRP





当收到创建 FDO 或筛选器驱动程序执行操作[ **IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766)请求相关联的 PDO，它可以只需将传递 IRP 到下一步低驱动程序或向下 IRP 传递之前执行特定操作。

### <a name="for-devices-that-support-wake-up"></a>支持唤醒的设备

一旦收到等待/唤醒 IRP，函数或筛选器驱动程序应执行以下步骤：

1.  调用[ **IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)，并传递当前 IRP，以确保该驱动程序不会接收即插即用[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)时处理等待/唤醒 IRP 的请求。

    如果[ **IoAcquireRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548204)返回失败状态，该驱动程序不应继续处理 IRP。 相反，它完成 IRP ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343))，并返回故障状态。

2.  检查处的值**Irp-&gt;Parameters.WaitWake.PowerState**并比较具有的当前设备电源状态**DeviceState**\[SystemWake\]中[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)结构。

    如果设备支持唤醒，但不能从指定[SystemWake](systemwake.md)状态或不是从当前设备电源状态，该驱动程序应失败 IRP，如下所示：

    -   将状态设置\_无效\_设备\_状态中**Irp-&gt;IoStatus.Status**。
    -   完成 IRP (**IoCompleteRequest**)，指定的 IO 优先级提升\_否\_增量。
    -   返回的状态设置**Irp-&gt;IoStatus.Status**从[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

3.  否则，设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) IRP 使用日常[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)。 *IoCompletion*例程应执行该驱动程序将设备恢复为工作状态所需的任何任务。

    *IoCompletion*如果取消 IRP，还将调用例程。

4.  保存驱动程序中可能需要的任何信息及其*IoCompletion*例程。

5.  调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336) （在 Windows 7 和 Windows Vista） 或[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) （在 Windows Server 003、 Windows XP 和 Windows 2000）若要将等待/唤醒 IRP 传递给下一个较低驱动程序。

6.  调用[ **IoReleaseRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549560)释放以前获取的锁。

7.  返回状态\_从 PENDING [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 该驱动程序不得更改中的值**Irp-&gt;IoStatus.Status**持有 IRP。

### <a name="for-devices-that-do-not-support-wake-up"></a>不支持唤醒的设备

如果函数或筛选器驱动程序收到等待/唤醒 IRP 设备不支持唤醒时，该驱动程序将失败，IRP，如下所示：

1.  完成 IRP (**IoCompleteRequest**)，指定的 IO 优先级提升\_否\_增量。

2.  返回的状态设置**Irp-&gt;IoStatus.Status**从[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

 

 




