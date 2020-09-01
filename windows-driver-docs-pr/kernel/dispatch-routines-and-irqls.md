---
title: Dispatch 例程和于 IRQL
description: Dispatch 例程和于 IRQL
ms.assetid: fe64e0f7-3906-470a-86c5-03460e652eed
keywords:
- 调度例程 WDK 内核，IRQLs
- IRQLs WDK 调度例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bfea6e9cdfcdf60d12483afc69754295abc338f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185651"
---
# <a name="dispatch-routines-and-irqls"></a>Dispatch 例程和于 IRQL





大多数驱动程序的调度例程在任何线程上下文的 IRQL = 被动级别调用 \_ ，但以下情况例外：

-   在发起 i/o 请求的线程的上下文（通常是用户模式应用程序线程）中，会调用任何最高级别的驱动程序的调度例程。

    换句话说，文件系统驱动程序和其他最高级别的驱动程序的调度例程在 nonarbitrary 线程上下文中以 IRQL = 被动级别进行调用 \_ 。

-   最低级别设备驱动程序的 [*DispatchRead*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 [*DispatchWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)和 [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程以及系统分页路径中其上方分层的中间驱动程序可在 IRQL = APC \_ 级别和任意线程上下文中调用。

    *DispatchRead*和/或*DispatchWrite*例程以及还处理此类最低级别设备或中间驱动程序中的读取和/或写入请求的任何其他例程必须始终处于驻留状态。 这些驱动程序例程既不可以分页，也不能成为驱动程序的可分页图像部分的一部分;它们不能访问任何可分页的内存。 而且，它们不应依赖于任何阻塞调用 (例如， [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 的) 不为零。

-   休眠和/或分页路径中的驱动程序的 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程可以以 IRQL = 调度级别进行调用 \_ 。 此类驱动程序的 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程必须准备好处理 PnP [**IRP \_ MN \_ 设备 \_ 使用 \_ 通知**](./irp-mn-device-usage-notification.md) 请求。

-   需要在启动时启用浪涌功能的驱动程序的 *DispatchPower* 例程可以在 IRQL = 调度级别调用 \_ 。

有关其他信息，请参阅 [管理硬件优先级](managing-hardware-priorities.md)。

 

