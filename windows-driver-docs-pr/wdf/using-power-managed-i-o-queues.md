---
title: 使用通过电源管理的 I/O 队列
description: 使用通过电源管理的 I/O 队列
keywords:
- I/o 队列-KMDF
- 电源管理 i/o 队列 WDK KMDF
- 重新排队参数 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6a798e29d57f3a4e741bb7de5f6aa550a3c69a4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814679"
---
# <a name="using-power-managed-io-queues"></a>使用通过电源管理的 I/O 队列


当驱动程序创建 i/o 队列时，它可以指定该队列是否经过 *电源管理*。 当电源管理队列中的 i/o 请求可用时，只有当设备处于工作状态 (D0) 状态时，框架才会将请求传递给驱动程序。 框架不允许设备保持其工作状态，直到已完成、取消或推迟框架从电源管理队列传递到驱动程序的所有 i/o 请求。

有关电源管理 i/o 队列的详细信息，请参阅 [电源管理以了解 I/o 队列](power-management-for-i-o-queues.md)。

## <a name="callback-functions-for-power-managed-queues"></a>Power-Managed 队列的回调函数


如果驱动程序使用电源管理的 i/o 队列，则可以提供其他两个回调函数：

<a href="" id="---------evtiostop"></a>[*EvtIoStop*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)  
[*EvtIoStop*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)回调函数停止处理指定的 i/o 请求。 当设备 (D0) 状态或已删除时，框架将为每个未 [完成](completing-i-o-requests.md)的 i/o 请求（包括驱动程序 [拥有](request-ownership.md)的请求以及该驱动程序已 [转发](forwarding-i-o-requests.md)到 i/o 目标的请求）调用一个 i/o 队列的 *EvtIoStop* 回调函数一次。

<a href="" id="---------evtioresume"></a>[*EvtIoResume*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)  
[*EvtIoResume*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)回调函数恢复处理以前停止的 i/o 请求。 在设备返回到其工作状态后，框架会调用 i/o 队列的 *EvtIoResume* 回调函数，从队列中恢复向驱动程序提供 i/o 请求。

当框架每次调用驱动程序的 [*EvtIoStop*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop) 回调函数时，该函数通常 [完成](completing-i-o-requests.md) 或 [取消](canceling-i-o-requests.md) i/o 请求，或调用 [**WdfRequestStopAcknowledge**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge) 将请求的所有权返回到框架。

虽然这是可选的，但通常情况下，应为电源管理的队列提供 [*EvtIoStop*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop) 回调函数。 通过提供 *EvtIoStop*，你的驱动程序有助于缩短设备之前所经过的时间，并使系统进入低功耗状态。

如果未提供电源管理队列的 [*EvtIoStop*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop) ，框架将等待，直到从电源管理的队列发送到驱动程序的所有请求都完成后，才能将设备移 (或系统) 降低到较低的电源状态或删除设备。 此延期可能会阻止系统进入其休眠状态或其他低系统电源状态。 在极端情况下，它可能会导致系统在错误代码9F 中崩溃。

如果你的驱动程序未将请求转发给 i/o 目标，并且没有在不确定的时间里持有请求，则可以安全地忽略 [*EvtIoStop*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop) 的管理队列。

## <a name="waiting-for-dispatcher-objects"></a>正在等待发送器对象


通常，驱动程序只应在 nonarbitrary 线程上下文内使用调度程序对象作为同步机制。

由于 [请求处理程序](request-handlers.md) 在任意线程上下文中运行，因此，电源管理的队列的请求处理程序不得等待设置内核调度程序对象。 这样做可能会导致死锁。

有关驱动程序何时可以等待调度程序对象的详细信息，以及当它无法使用时该如何操作的详细信息，请参阅 [内核调度程序对象简介](../kernel/introduction-to-kernel-dispatcher-objects.md)。

 

