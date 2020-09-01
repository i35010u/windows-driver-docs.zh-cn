---
title: 处理 IRP_MN_CANCEL_STOP_DEVICE 请求（Windows 2000 和更高版本）
description: 处理 IRP_MN_CANCEL_STOP_DEVICE 请求（Windows 2000 和更高版本）
ms.assetid: 2e5e835f-d327-4bde-bdfd-8a71a47b0ac0
keywords:
- IRP_MN_CANCEL_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0a53bfd2d1ead199d10ae004fc874c946f35775
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183857"
---
# <a name="handling-an-irp_mn_cancel_stop_device-request-windows-2000-and-later"></a>处理 IRP \_ MN \_ CANCEL \_ 停止 \_ 设备请求 (Windows 2000 和更高版本) 





必须首先由设备的父总线驱动程序和设备堆栈中的每个更高的驱动程序处理 [**IRP \_ MN \_ CANCEL \_ 停止 \_ 设备**](./irp-mn-cancel-stop-device.md) 请求。 驱动程序处理其 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中的停止 irp。

为了响应 **IRP \_ MN \_ CANCEL \_ 停止 \_ 设备** 请求，驱动程序必须将设备返回到其已启动状态并恢复正常操作。 驱动程序必须成功完成取消-停止 IRP。

驱动程序使用如下所示的过程来处理 **IRP \_ MN \_ CANCEL \_ 停止 \_ 设备** 请求：

1.  在较低的驱动程序完成其重新启动操作之前，请推迟重新启动设备。  (请参阅 [推迟 PNP IRP 处理，直到驱动程序的驱动程序完成](postponing-pnp-irp-processing-until-lower-drivers-finish.md)。 ) 

2.  在较低的驱动程序完成后，将设备恢复到其启动状态。

    具体操作取决于设备和驱动程序。

3.  在 IRP 中启动 irp-保存队列。

    如果驱动程序在设备处于停止挂起状态时包含请求，请清除 "保留 \_ 新 \_ 请求" 标志，并在 IRP 保留队列中启动 irp。 有关详细信息，请参阅 [在设备暂停时保留传入 irp](holding-incoming-irps-when-a-device-is-paused.md) 。

4.  完成 IRP with [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)。

    -   在函数或筛选器驱动程序中：

        驱动程序的 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程返回状态 \_ \_ "需要更多 \_ 的处理"，如 [推迟 PnP IRP 处理，直到驱动程序的完成时间下降](postponing-pnp-irp-processing-until-lower-drivers-finish.md)，因此驱动程序的 *DispatchPnP* 例程必须调用 **IoCompleteRequest** 才能恢复 i/o 完成处理。

        驱动程序将 **Irp- &gt; IoStatus** 设置为状态 \_ SUCCESS，调用 **IoCompleteRequest** ，同时提升 IO \_ 无 \_ 增量，并 \_ 从其 *DispatchPnP* 例程返回状态 success。

        驱动程序不能使此操作失败。 如果驱动程序未能重新启动 IRP，则设备处于不一致状态，并且不会正常运行。

    -   在父总线驱动程序中：

        驱动程序将 **Irp- &gt; IoStatus** 设置为 status \_ SUCCESS，并调用 **IoCompleteRequest** 来指定 IO 无增量的优先级提升 \_ \_ 。 总线驱动程序 \_ 从其 *DispatchPnP* 例程返回状态 SUCCESS。

        总线驱动程序不能使此操作失败。 如果驱动程序未能重新启动 IRP，则设备处于不一致状态，并且不会正常运行。

设备启动并处于活动状态时，驱动程序可能会收到虚假的取消-停止请求。 例如，如果驱动程序 (或设备堆栈中较高版本的驱动程序，则可能会发生这种情况) [**IRP \_ MN \_ 查询 \_ 停止 \_ 设备**](./irp-mn-query-stop-device.md) 请求。 设备启动并处于活动状态时，驱动程序可以安全地成功为设备执行虚假的取消停止请求。

 

