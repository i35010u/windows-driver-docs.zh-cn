---
title: 设备暂停时保持传入的 IRP
description: 设备暂停时保持传入的 IRP
keywords:
- 保存 Irp
- Irp WDK PnP
- I/o 请求数据包 WDK PnP
- 暂停 PnP 设备
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12bf466b05aa8bfcbf512dcf12ce4da0e4080004
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837713"
---
# <a name="holding-incoming-irps-when-a-device-is-paused"></a>设备暂停时保持传入的 IRP





设备的驱动程序必须在重新平衡其资源时暂停设备。 在资源重新平衡过程中，某些驱动程序会暂停设备以响应 [**IRP \_ MN \_ 查询 \_ 停止 \_ 设备**](./irp-mn-query-stop-device.md) 请求，其他驱动程序会延迟设备暂停，直到收到 [**IRP \_ MN \_ 停止 \_ 设备**](./irp-mn-stop-device.md) 请求。 在任一情况下，如果 **IRP \_ MN \_ 停止 \_ 设备** 成功，设备必须暂停。

驱动程序必须完成设备上正在进行的任何 Irp，并避免启动任何需要访问该设备的新 Irp。

若要在设备暂停时保存 Irp，驱动程序将实现如下所示的过程：

1.  在其 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程中，使用类似于 "保留新请求" 的名称在设备扩展中定义一个标志 \_ \_ 。 清除标志。

2.  创建用于保存 Irp 的 FIFO 队列。

    如果驱动程序已经对 Irp 进行了排队，则它可以重复使用同一队列，因为在暂停设备之前需要驱动程序来完成所有未完成的请求。

    如果驱动程序还没有 IRP 队列，则必须在其 *AddDevice* 例程中创建一个。 它所创建的队列类型取决于驱动程序刷新队列的方式。 驱动程序可以使用联锁的双向链接列表和 **ExInterlocked *Xxx* 列表** 例程。

3.  在其 *DispatchPnP* 代码中， **irp \_ MN \_ 查询 \_ 停止 \_ 设备** (或 **IRP \_ MN \_ 停止 \_ 设备**) ，完成所有未完成的请求并设置保留 \_ 新 \_ 请求标志。

4.  在访问设备的调度例程（如 [*DispatchWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 或 [*DispatchRead*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)）中，检查是否设置了 "保持 \_ 新请求" \_ 标志。 如果是这样，则驱动程序必须将 IRP 标记为 "正在挂起" 并将其排队。

    驱动程序的 *DispatchPnP* 例程必须继续处理 PnP irp，而不是保留它们， [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程必须继续处理电源 irp。

5.  在 *DispatchPnP* 中，若要响应启动或取消停止 IRP，请清除 "保留 \_ 新 \_ 请求" 标志，并在 IRP 保留队列中启动 irp。

    这些操作可能是处理这些 PnP Irp 的最后步骤。 例如，为了响应启动 IRP，驱动程序必须首先执行任何操作来启动设备，然后它可以在 IRP 持有的队列中启动 Irp。

    处理 IRP 的 irp 时，处理 irp 中的错误不会影响为启动或取消停止 Irp 返回的状态。

 

