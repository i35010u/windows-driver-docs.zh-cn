---
title: 管理 I/O 队列
description: 管理 I/O 队列
ms.assetid: 83cc87c8-7e2d-4f79-a580-0519d327e7ba
keywords:
- I/o 队列 WDK KMDF，开始
- I/o 队列 WDK KMDF，停止
- I/o 队列 WDK KMDF，重新启动
- I/o 队列 WDK KMDF，添加请求
- I/o 队列 WDK KMDF，获取请求
- I/o 队列 WDK KMDF，搜索请求
- I/o 队列 WDK KMDF，清除
- I/o 队列 WDK KMDF，排出
- I/o 队列 WDK KMDF，移动请求
- I/o 队列 WDK KMDF，截获请求
- I/o 队列 WDK KMDF，属性
- 截获 i/o 请求 WDK KMDF
- 移动 i/o 请求 WDK KMDF
- 重定位 i/o 请求 WDK KMDF
- 搜索 i/o 请求 WDK KMDF
- 正在重新排队 i/o 请求 WDK KMDF
- 停止 i/o 队列 WDK KMDF
- 重新启动 i/o 队列 WDK KMDF
- 启动 i/o 队列 WDK KMDF
- 调度方法 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f615f67236b5691246b6183c731b92bd4f4f2f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843152"
---
# <a name="managing-io-queues"></a>管理 I/O 队列


## <a href="" id="starting-an-i-o-queue"></a>启动 i/o 队列


当驱动程序调用[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)来创建 i/o 队列时，框架会自动使队列接收 i/o 请求并将其传递给驱动程序。

驱动程序通常从[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数中调用[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate) 。 当驱动程序的*EvtDriverDeviceAdd*回调函数返回后，框架可以开始向驱动程序提供 i/o 请求。

如果你的驱动程序使用[电源管理](using-power-managed-i-o-queues.md)的 i/o 队列，则在设备进入其工作状态并且框架已调用驱动程序的[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调函数之前，框架无法开始向你的驱动程序提供请求。

## <a href="" id="stopping-and-restarting-an-i-o-queue"></a>停止并重新启动 i/o 队列


你的驱动程序可以调用[**WdfIoQueueStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)或[**WdfIoQueueStopSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopsynchronously)来暂时阻止框架从 i/o 队列传递 i/o 请求。 若要恢复 i/o 请求的传送，驱动程序将调用[**WdfIoQueueStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestart)。

如果驱动程序使用电源管理的 i/o 队列，则当设备离开其工作（D0）状态时，框架会自动停止设备的队列，当设备状态返回到 D0 时，框架将重新启动队列。

## <a href="" id="adding-requests-to-an-i-o-queue"></a>向 i/o 队列添加请求


当系统将读取、写入或设备 i/o 控制请求发送到驱动程序时，框架会将请求放入 i/o 队列。 驱动程序可以通过调用[**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)来控制框架在每个队列中存储的请求的类型。

驱动程序还可以通过调用[**WdfRequestForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)，重新排队从框架收到的请求。

## <a href="" id="obtaining-requests-from-an-i-o-queue"></a>从 i/o 队列获取请求


如果驱动程序为 i/o 队列指定了顺序或并行[调度方法](dispatching-methods-for-i-o-requests.md)，则它将在[请求处理程序](request-handlers.md)中收到请求。

如果驱动程序指定了手动或顺序调度方法，则可以通过调用[**WdfIoQueueRetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievenextrequest)或[**WdfIoQueueRetrieveRequestByFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrieverequestbyfileobject)获取请求。

## <a href="" id="searching-for-an-i-o-request"></a>搜索 i/o 请求


如果驱动程序为 i/o 队列指定手动[调度方法](dispatching-methods-for-i-o-requests.md)，则可以使用以下步骤在队列中搜索特定的请求：

1.  调用[**WdfIoQueueFindRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuefindrequest)以查找与驱动程序指定的条件匹配的请求。

2.  调用[**WdfIoQueueRetrieveFoundRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest)可检索[**WdfIoQueueFindRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuefindrequest)找到的请求。

## <a href="" id="purging-or-draining-an-i-o-queue"></a>清除或排出 i/o 队列


*清除*i/o 队列意味着停止将 i/o 请求插入到队列中，并取消队列中已有的任何请求。

*排出*i/o 队列意味着停止将 i/o 请求插入到队列中，同时允许将队列中已经存在的任何请求传递到该驱动程序。

通常，驱动程序只会在队列不受电源管理的情况下清除或清空队列。 对于电源托管 i/o 队列，驱动程序可以提供[*EvtIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)和[*EvtIoResume*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)回调函数。

如果某些驱动程序的队列不是电源管理的，则可能要在其关联的设备或 i/o 通道变为不可用时清除或清空队列。 通常情况下，会清除队列，而不是释放队列，除非每个请求的可能性很高，因为每个请求都包含非常重要的信息。 例如，网络设备的驱动程序可能会清除其队列，而存储设备的驱动程序可能会耗尽其队列。

如果希望驱动程序清除或清空 i/o 队列，驱动程序可以调用以下队列对象方法之一：

-   [**WdfIoQueuePurge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurge)或[**WdfIoQueuePurgeSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)，用于停止对 i/o 队列发出的 i/o 请求并取消未处理的请求。

-   [**WdfIoQueueDrain**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrain)或[**WdfIoQueueDrainSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)，用于停止将 i/o 请求排队到 i/o 队列，同时允许传递和处理已排队的请求。

调用[**WdfIoQueueDrain**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrain)和[**WdfIoQueueDrainSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)时要格外小心。 由于排出操作会等待请求完成，因此，仅当确信队列的挂起请求将及时完成时，才应排出队列。 如果你不知道 i/o 请求需要多长时间才能完成，并且可接受取消未处理的请求，请考虑清除队列。

## <a href="" id="moving-requests-from-one-i-o-queue-to-another"></a>将请求从一个 i/o 队列移动到另一个 i/o 队列


当你的驱动程序收到 i/o 请求后，你可能希望驱动程序将请求重新排队到不同的 i/o 队列。 为此，驱动程序将调用[**WdfRequestForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)或[**WdfRequestForwardToParentDeviceIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoparentdeviceioqueue)，这会将请求添加到指定队列的尾部。 最终，该框架将使用指定的队列调度方法再次将请求传递给驱动程序。 有关将 i/o 请求从一个 i/o 队列移到另一个队列的详细信息，请参阅[正在重新排队 I/o 请求](requeuing-i-o-requests.md)。

## <a href="" id="intercepting-an-i-o-request-before-it-is-queued"></a>正在截获 i/o 请求，并将其排入队列


驱动程序在框架将请求放入 i/o 队列之前，可能会截获 i/o 请求。 若要截获 i/o 请求，驱动程序必须调用[**WdfDeviceInitSetIoInCallerContextCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetioincallercontextcallback)来注册[*EvtIoInCallerContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)回调函数。

框架将[*EvtIoInCallerContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)回调函数与设备相关联。 因此，每次收到系统发送到设备的请求时，框架都会调用*EvtIoInCallerContext*回调函数。

通常，当[*EvtIoInCallerContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)回调函数收到请求时，它将为请求执行一些初步处理。 接下来，回调函数调用[**WdfDeviceEnqueueRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)，后者向框架返回请求。 然后，框架可以将请求置于正确的 i/o 队列中，就像它未调用*EvtIoInCallerContext*回调函数一样。

驱动程序提供[*EvtIoInCallerContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)回调函数的主要原因是，驱动程序必须处理支持非缓冲的 i/o 方法[和直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers#neither)的 i/o 操作。 对于此 i/o 方法，驱动程序必须在 i/o 请求的发起方的进程上下文中访问接收的缓冲区。 有关详细信息，请参阅[在基于框架的驱动程序中访问数据缓冲区](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)。

## <a href="" id="obtaining-i-o-queue-properties"></a>获取 i/o 队列属性


若要获取框架队列对象的属性，驱动程序可以调用以下方法：

-   [**WdfIoQueueGetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuegetdevice)，用于获取队列对象所属的设备对象的句柄。

-   [**WdfIoQueueGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuegetstate)，用于获取有关队列的[状态信息](i-o-queue-states.md)。

 

 





