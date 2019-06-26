---
title: Dispatch 例程和于 IRQL
description: Dispatch 例程和于 IRQL
ms.assetid: fe64e0f7-3906-470a-86c5-03460e652eed
keywords:
- 调度例程 WDK 内核，于 Irql
- 于 Irql WDK 调度例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ad3e092e90b114f506d63f09aafa79a591c1f2a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384984"
---
# <a name="dispatch-routines-and-irqls"></a>Dispatch 例程和于 IRQL





大多数驱动程序的调度例程调用中的任意线程上下文在 IRQL = 被动\_级别，但存在以下例外：

-   发起 I/O 请求，这通常是用户模式应用程序线程的线程的上下文中调用任何最高级别的驱动程序的调度例程。

    换而言之，在 IRQL nonarbitrary 线程上下文中调用的文件系统驱动程序和其他最高级别的驱动程序的调度例程 = 被动\_级别。

-   [ *DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)， [ *DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)，并[ *DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程的最低级别的设备驱动程序和中间驱动程序的上面它们在系统分页路径中，可以调用在 IRQL = APC\_级别和在任意线程上下文中。

    *DispatchRead*和/或*DispatchWrite*例程和任何其他例程，还进程读取和/或写入请求，在这种最低级别的设备或中间驱动程序，必须驻留在所有时间。 这些驱动程序例程可以既不是可分页，也不能属于一个驱动程序的可分页图像部分;它们必须访问的任何可分页内存。 此外，它们不应依赖于任何阻止调用 (如[ **KeWaitForSingleObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)使用非零的超时值)。

-   [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程休眠和/或分页路径中的驱动程序可以调用在 IRQL = 调度\_级别。 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程的此类驱动程序必须准备好处理即插即用[ **IRP\_MN\_设备\_用法\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)请求。

-   *DispatchPower*例程需要在启动时的浪涌电源的驱动程序可以调用在 IRQL = 调度\_级别。

有关其他信息，请参阅[管理硬件优先级](managing-hardware-priorities.md)。

 

 




