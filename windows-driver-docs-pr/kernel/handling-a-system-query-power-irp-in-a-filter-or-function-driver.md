---
title: 处理筛选器或函数驱动程序中的系统 Query-Power IRP
description: 处理筛选器或函数驱动程序中的系统 Query-Power IRP
ms.assetid: 81d921d5-6db8-4858-b86e-1484781faba5
keywords:
- 查询-power Irp WDK 电源管理
- 筛选器驱动程序 WDK 电源管理
- 函数驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75aa2e3a93acbd6a939feb93c8f40951f99b7ec2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836617"
---
# <a name="handling-a-system-query-power-irp-in-a-filter-or-function-driver"></a>处理筛选器或函数驱动程序中的系统 Query-Power IRP





筛选器或函数驱动程序（不是设备的电源策略所有者）应将系统查询-power IRP 传递到下一个较低版本的驱动程序，请执行以下步骤：

1.  调用[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)，传递当前 IRP，以确保驱动程序未收到 PnP [**IRP\_MN\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)在处理 power IRP 时删除\_设备请求。

    如果**IoAcquireRemoveLock**返回失败状态，驱动程序不应继续处理 IRP。 从 Windows Vista 开始，驱动程序应调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)来完成 IRP 并返回失败状态。 在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序应调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)，并调用**IOCOMPLETEREQUEST**来完成 IRP，并返回失败状态。

2.  确定查询是否应失败。 有关指南，请参阅[在筛选器或函数驱动程序中失败系统查询-POWER IRP](failing-a-system-query-power-irp-in-a-filter-or-function-driver.md) ，并按该部分所述完成处理。

3.  调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)。 （仅限 windows Server 2003、Windows XP 和 Windows 2000）

4.  设置 IRP 堆栈位置（[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)或[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)）。 驱动程序可以在 IRP 中设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，但这样做很少需要。

5.  调用**IoCallDriver** （在 windows 7 和 windows Vista 中）或[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) （在 Windows SERVER 2003、windows XP 和 windows 2000 中）将 IRP 传递到下一个较低版本的驱动程序。

6.  调用[**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)。 但是，如果驱动程序为 IRP 设置*IoCompletion*例程，则改为从*IoCompletion*例程进行此调用。

7.  返回状态从其[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程挂起\_。

 

 




