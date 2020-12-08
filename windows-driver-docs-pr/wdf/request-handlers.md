---
title: 请求处理程序
description: 请求处理程序
keywords:
- I/o 队列 WDK KMDF，创建
- I/o 队列 WDK KMDF，请求处理程序
- 请求处理程序 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6234a16c2da0624887b0f1473296cbb12d8e510d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821721"
---
# <a name="request-handlers"></a>请求处理程序





如果你的驱动程序为 i/o 队列指定了顺序或并行 [调度方法](dispatching-methods-for-i-o-requests.md) ，则该框架将在每次准备向驱动程序提供队列请求之一时调用驱动程序提供的回调函数。

对于每个 i/o 队列，驱动程序可以提供以下一个或多个称为 *请求处理程序* 的回调函数：

<a href="" id="evtioread"></a>[*EvtIoRead*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)  
当队列中有可用的读取请求时，框架将调用 i/o 队列的 [*EvtIoRead*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read) 回调函数。

<a href="" id="evtiowrite"></a>[*EvtIoWrite*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)  
当队列中有写入请求时，框架将调用 i/o 队列的 [*EvtIoWrite*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write) 回调函数。

<a href="" id="evtiodevicecontrol"></a>[*EvtIoDeviceControl*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)  
当设备 i/o 控制请求在队列中可用时，框架会调用 i/o 队列的 [*EvtIoDeviceControl*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control) 回调函数。

<a href="" id="evtiointernaldevicecontrol"></a>[*EvtIoInternalDeviceControl*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)  
当队列中有内部设备 i/o 控制请求可用时，框架会调用 i/o 队列的 [*EvtIoInternalDeviceControl*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control) 回调函数。

<a href="" id="evtiodefault"></a>[*EvtIoDefault*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)  
如果该驱动程序未提供关联的特定于请求类型的回调函数，则在有任何可用请求时，框架将调用 i/o 队列的 [*EvtIoDefault*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default) 回调函数。

驱动程序在调用 [**WdfIoQueueCreate**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate) 以为设备创建 i/o 队列时注册回调函数。

其中每个回调函数都接收两个输入参数：框架要传递给驱动程序的 i/o 请求的句柄，以及包含请求的 i/o 队列的句柄。 回调函数可以通过调用 [**WdfIoQueueGetDevice**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuegetdevice)来确定目标设备。

框架在任意线程上下文中调用驱动程序的请求处理程序。 在任意线程上下文中执行时，驱动程序不应等待很长一段时间。 在某些情况下，驱动程序可能使用内核调度程序对象作为同步机制。 有关驱动程序何时可以等待调度程序对象的信息，以及在无法进行操作时要执行的操作，请参阅 [内核调度程序对象简介](../kernel/introduction-to-kernel-dispatcher-objects.md)。

 

