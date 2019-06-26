---
title: 管理 I/O 队列
description: 管理 I/O 队列
ms.assetid: 83cc87c8-7e2d-4f79-a580-0519d327e7ba
keywords:
- I/O 队列 WDK KMDF，启动
- I/O 队列 WDK KMDF，停止
- I/O 队列 WDK KMDF，重新启动
- I/O 队列 WDK KMDF，添加请求
- I/O 队列 WDK KMDF，获取请求
- I/O 队列 WDK KMDF，搜索请求
- I/O 队列 WDK KMDF，清除
- WDK KMDF，清空的 I/O 队列
- I/O 队列 WDK KMDF，移动请求
- I/O 队列 WDK KMDF，拦截请求
- I/O 队列 WDK KMDF，属性
- 截获 I/O 请求 WDK KMDF
- 移动 I/O 请求 WDK KMDF
- 重新定位 I/O 请求 WDK KMDF
- 搜索 I/O 请求 WDK KMDF
- 排队 I/O 请求 WDK KMDF
- 正在停止 I/O 队列 WDK KMDF
- 重新启动 I/O 队列 WDK KMDF
- 启动 I/O 队列 WDK KMDF
- 调度方法 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8776f020377a86ec753a85cb0d2350ff200e52bf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371729"
---
# <a name="managing-io-queues"></a>管理 I/O 队列


## <a href="" id="starting-an-i-o-queue"></a> 启动 I/O 队列


当驱动程序调用[ **WdfIoQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuecreate)若要创建的 I/O 队列，该框架会自动启用队列接收的 I/O 请求并将其交付到驱动程序。

通常情况下，驱动程序调用[ **WdfIoQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuecreate)中[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。 该框架可以开始在驱动程序后将 I/O 请求传递到驱动程序*EvtDriverDeviceAdd*回调函数返回。

如果使用您的驱动程序[电源管理](using-power-managed-i-o-queues.md)I/O 队列，该框架不能以将请求传递到您的驱动程序，直到在设备进入其工作状态并在 framework 已调用了驱动程序的[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调函数。

## <a href="" id="stopping-and-restarting-an-i-o-queue"></a> 停止并重新启动 I/O 队列


您的驱动程序可以调用[ **WdfIoQueueStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestop)或[ **WdfIoQueueStopSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopsynchronously)以临时阻止的框架，从 I/O 队列传送 I/O 请求。 若要恢复的 I/O 请求的传递，该驱动程序调用[ **WdfIoQueueStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestart)。

如果您的驱动程序使用电源管理的 I/O 队列，该框架将设备使其工作 (D0) 状态，且时设备状态返回到 D0 框架中的队列、 重新启动时自动停止设备的队列。

## <a href="" id="adding-requests-to-an-i-o-queue"></a> 将请求添加到的 I/O 队列


时系统将读取、 写入或设备的 I/O 控制请求发送到驱动程序，该框架将 I/O 队列中放置请求。 该驱动程序可以控制该框架通过调用来存储每个队列中的请求的类型[ **WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)。

驱动程序还可以重新排队请求它已收到了框架，通过调用[ **WdfRequestForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)。

## <a href="" id="obtaining-requests-from-an-i-o-queue"></a> 从 I/O 队列获取请求


如果驱动程序指定的顺序或并行[调度方法](dispatching-methods-for-i-o-requests.md)I/O 队列，它接收的请求中的[请求处理程序](request-handlers.md)。

如果驱动程序指定手动或顺序调度方法，它可以获取请求通过调用[ **WdfIoQueueRetrieveNextRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrievenextrequest)或[ **WdfIoQueueRetrieveRequestByFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrieverequestbyfileobject)。

## <a href="" id="searching-for-an-i-o-request"></a> 搜索 I/O 请求


如果驱动程序指定手动[调度方法](dispatching-methods-for-i-o-requests.md)I/O 队列，它可以使用以下步骤以在队列中的特定请求搜索：

1.  调用[ **WdfIoQueueFindRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuefindrequest)来查找与驱动程序指定条件匹配的请求。

2.  调用[ **WdfIoQueueRetrieveFoundRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest)检索请求的[ **WdfIoQueueFindRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuefindrequest)位于。

## <a href="" id="purging-or-draining-an-i-o-queue"></a> 清除或清空 I/O 队列


*清除*I/O 队列意味着正在插入到队列中的 I/O 请求停止和取消队列中已有的任何请求。

*排出*I/O 队列意味着停止插入输入/输出请求到的队列，同时允许要传递到驱动程序的队列中已有的任何请求。

驱动程序通常清除或清空其队列，仅当队列不是电源管理。 对于电源管理的 I/O 队列，驱动程序可以提供[ *EvtIoStop* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)并[ *EvtIoResume* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)回调函数。

如果某些驱动程序的队列不是电源管理，你可能想要清除或清空队列，如果其关联的设备或 I/O 通道变得不可用。 通常情况下，将清除，而不是排出、 队列除非很可能存在的每个请求包含非常重要的信息。 例如，网络设备的驱动程序可能会清除其队列，而存储设备的驱动程序可能会清空其队列。

如果您希望您的驱动程序以清除或清空 I/O 队列，该驱动程序可以调用以下的队列对象方法之一：

-   [**WdfIoQueuePurge** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurge)或[ **WdfIoQueuePurgeSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)，以停止队列对 I/O 队列的 I/O 请求并取消未处理的请求。

-   [**WdfIoQueueDrain** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrain)或[ **WdfIoQueueDrainSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)，若要停止队列同时允许已排队的请求传递到 I/O 队列的 I/O 请求和处理。

调用时多加小心[ **WdfIoQueueDrain** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrain)并[ **WdfIoQueueDrainSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)。 因为清空操作在等待完成请求，应仅清空队列，如果您确定队列的挂起的请求将及时完成。 如果不知道长时间 I/O 请求后要完成花费的时间，它是可以接受取消未完成的请求，请考虑清除队列。

## <a href="" id="moving-requests-from-one-i-o-queue-to-another"></a> 将请求从一个 I/O 队列移动到另一个


您的驱动程序已收到的 I/O 请求后，可能想要将请求到不同的 I/O 队列重新排队的驱动程序。 若要执行此操作，驱动程序调用[ **WdfRequestForwardToIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)或[ **WdfRequestForwardToParentDeviceIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestforwardtoparentdeviceioqueue)，这会增加请求到指定的队列的末尾。 最终，框架将传送该请求向驱动程序再次通过使用指定的队列的调度方法。 有关将 I/O 请求从一个 I/O 队列移动到另一个详细信息，请参阅[排队 I/O 请求](requeuing-i-o-requests.md)。

## <a href="" id="intercepting-an-i-o-request-before-it-is-queued"></a> 已排队之前截获 I/O 请求


很可能在 framework 中的 I/O 队列放入请求之前截获的 I/O 请求的驱动程序。 若要截获 I/O 请求，该驱动程序必须调用[ **WdfDeviceInitSetIoInCallerContextCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetioincallercontextcallback)注册[ *EvtIoInCallerContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)回调函数。

该框架将相关联[ *EvtIoInCallerContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)与设备的回调函数。 因此，框架将调用*EvtIoInCallerContext*回调函数，每当它收到的请求的系统发送到设备。

通常，当[ *EvtIoInCallerContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)回调函数收到请求时，它执行一些初步处理请求。 接下来，调用的回调函数[ **WdfDeviceEnqueueRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)，这将给予请求返回框架。 框架可以然后将请求放在正确的 I/O 队列中，就像在不调用了*EvtIoInCallerContext*回调函数。

驱动程序可能会提供的主要原因[ *EvtIoInCallerContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)驱动程序必须处理 I/O 操作支持 I/O 方法调用的回调函数是[既不缓冲，也不直接 I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers#neither)。 对于此 I/O 方法，该驱动程序必须访问的 I/O 请求的发起进程上下文中的接收的缓冲区。 有关详细信息，请参阅[基于 Framework 的驱动程序中访问数据缓冲区](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)。

## <a href="" id="obtaining-i-o-queue-properties"></a> 获取 I/O 队列属性


若要获取 framework 队列对象的属性，该驱动程序可以调用以下方法：

-   [**WdfIoQueueGetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuegetdevice)，以获取对队列对象所属的设备对象的句柄。

-   [**WdfIoQueueGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuegetstate)，以获取[的状态信息](i-o-queue-states.md)有关队列。

 

 





