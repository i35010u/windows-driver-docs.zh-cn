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
ms.openlocfilehash: 33d0b8a6370ca8343e8e3b77686e290c1d2cfc85
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191363"
---
# <a name="handling-a-system-query-power-irp-in-a-filter-or-function-driver"></a>处理筛选器或函数驱动程序中的系统 Query-Power IRP





不是设备的电源策略所有者 (筛选器或函数驱动程序) 应将系统查询-power IRP 传递到下一个较低版本的驱动程序，请执行以下步骤：

1.  调用 [**IoAcquireRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)，传递当前 IRP，以确保在处理 power irp 时，驱动程序不会收到 PnP [**IRP \_ MN \_ 删除 \_ 设备**](./irp-mn-remove-device.md) 请求。

    如果 **IoAcquireRemoveLock** 返回失败状态，驱动程序不应继续处理 IRP。 从 Windows Vista 开始，驱动程序应调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 来完成 IRP 并返回失败状态。 在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序应调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)，并调用 **IOCOMPLETEREQUEST** 来完成 IRP，并返回失败状态。

2.  确定查询是否应失败。 有关指南，请参阅 [在筛选器或函数驱动程序中失败系统查询-POWER IRP](failing-a-system-query-power-irp-in-a-filter-or-function-driver.md) ，并按该部分所述完成处理。

3.  调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)。 仅 (Windows Server 2003、Windows XP 和 Windows 2000) 

4.  将 IRP 堆栈位置 ([**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md) 或 [**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)) 。 驱动程序可以在 IRP 中设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，但这样做很少需要。

5.  在 windows 7 和 Windows Vista 中调用 **IoCallDriver** () 或 windows Server 2003、windows XP 和 windows 2000 中的 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) () 将 IRP 传递到下一个较低版本的驱动程序。

6.  调用 [**IoReleaseRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)。 但是，如果驱动程序为 IRP 设置 *IoCompletion* 例程，则改为从 *IoCompletion* 例程进行此调用。

7.  \_从其[*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程返回的状态为 "挂起"。

 

