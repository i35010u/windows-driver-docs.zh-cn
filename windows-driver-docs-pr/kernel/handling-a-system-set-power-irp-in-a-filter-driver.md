---
title: 处理筛选器驱动程序中的系统 Set-Power IRP
description: 处理筛选器驱动程序中的系统 Set-Power IRP
ms.assetid: a6e364fc-f173-47ce-b36b-84f802cefcc3
keywords:
- 设置 power Irp WDK 电源管理
- 筛选器驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 896993bd5712411a84b734e1057825625dc45c60
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384246"
---
# <a name="handling-a-system-set-power-irp-in-a-filter-driver"></a>处理筛选器驱动程序中的系统 Set-Power IRP





所有筛选器驱动程序以及不属于其设备堆栈的电源策略的任何功能驱动程序应只需传递系统集 power IRP 到下一步低驱动程序，在以下步骤：

1.  调用[ **IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)，并传递当前 IRP，以确保该驱动程序不会接收即插即用[ **IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求，而同时处理 IRP 的能力。

    如果**IoAcquireRemoveLock**返回失败状态，该驱动程序不应继续处理 IRP。 相反，从 Windows Vista 开始，驱动程序应调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)完成 IRP 并返回故障状态。 在 Windows Server 2003、 Windows XP 和 Windows 2000 中，该驱动程序首先应调用[ **PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)，调用**IoCompleteRequest**完成 IRP，，然后返回故障状态。

2.  调用**PoStartNextPowerIrp**启动下一个幂 IRP。 （Windows Server 2003、 Windows XP 和 Windows 2000 仅。）

3.  设置 IRP 堆栈位置 ([**IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)或[ **IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext))。 该驱动程序可以设置[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程中 IRP，但这样很少需要。

4.  调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) （在 Windows 7 和 Windows Vista） 或[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) （在 Windows Server 2003、 Windows XP 和 Windows 2000）若要将 IRP 传递给下一个较低驱动程序。

5.  调用[ **IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)。 但是，如果该驱动程序设置[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程 IRP，进行此调用，从*IoCompletion*例程相反。

6.  返回状态\_PENDING 从其[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

 

 




