---
title: 处理筛选器驱动程序中的系统 Set-Power IRP
description: 处理筛选器驱动程序中的系统 Set-Power IRP
keywords:
- 设置电源 Irp WDK 电源管理
- 筛选器驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5f7f3c6de0938cf565de2e751f589f705db94c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792725"
---
# <a name="handling-a-system-set-power-irp-in-a-filter-driver"></a>处理筛选器驱动程序中的系统 Set-Power IRP





所有筛选器驱动程序和不拥有其设备堆栈的电源策略的任何函数驱动程序都应该只需将系统设置-电源 IRP 传递到下一个较低的驱动程序，如下所示：

1.  调用 [**IoAcquireRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)，传递当前 IRP，以确保在处理 power irp 时，驱动程序不会收到 PnP [**IRP \_ MN \_ 删除 \_ 设备**](./irp-mn-remove-device.md) 请求。

    如果 **IoAcquireRemoveLock** 返回失败状态，驱动程序不应继续处理 IRP。 从 Windows Vista 开始，驱动程序应调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 来完成 IRP 并返回失败状态。 在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序应该首先调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)，然后调用 **IOCOMPLETEREQUEST** 来完成 IRP，然后返回失败状态。

2.  调用 **PoStartNextPowerIrp** 以启动下一个 power IRP。 仅 (Windows Server 2003、Windows XP 和 Windows 2000。 ) 

3.  将 IRP 堆栈位置 ([**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md) 或 [**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)) 。 驱动程序可以在 IRP 中设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，但这样做很少需要。

4.  在 windows 7 和 Windows Vista 中调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) () 或 windows Server 2003、windows XP 和 windows 2000 中的 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) () 将 IRP 传递到下一个较低版本的驱动程序。

5.  调用 [**IoReleaseRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)。 但是，如果驱动程序为 IRP 设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，则改为从 *IoCompletion* 例程进行此调用。

6.  \_从其 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程返回的状态为 "挂起"。

 

