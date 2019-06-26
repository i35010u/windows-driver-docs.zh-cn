---
title: 请求处理程序
description: 请求处理程序
ms.assetid: bfc543bf-18a8-4e2c-ba7a-d0a21cefb038
keywords:
- I/O 队列 WDK KMDF，创建
- I/O 队列 WDK KMDF 请求处理程序
- 请求处理程序 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af70dbb2c27f1f24334d50f8099c0e8a6345664a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376278"
---
# <a name="request-handlers"></a>请求处理程序





如果您的驱动程序已指定的顺序或并行[调度方法](dispatching-methods-for-i-o-requests.md)I/O 队列，框架调用驱动程序提供的回调函数每次它已准备好将其中一个队列的请求传递到驱动程序。

对于每个 I/O 队列，该驱动程序可以提供一个或多个以下的回调函数，称为*请求处理程序*:

<a href="" id="evtioread"></a>[*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)  
框架将调用的 I/O 队列[ *EvtIoRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)回调函数的读取的请求时在队列中可用。

<a href="" id="evtiowrite"></a>[*EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)  
框架将调用的 I/O 队列[ *EvtIoWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)写入请求在队列中可用时的回调函数。

<a href="" id="evtiodevicecontrol"></a>[*EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)  
框架将调用的 I/O 队列[ *EvtIoDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)设备 I/O 控制请求在队列中可用时的回调函数。

<a href="" id="evtiointernaldevicecontrol"></a>[*EvtIoInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)  
框架将调用的 I/O 队列[ *EvtIoInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)回调函数内部设备 I/O 控制请求在队列中不可用。

<a href="" id="evtiodefault"></a>[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)  
框架将调用的 I/O 队列[ *EvtIoDefault* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)回调函数的任何请求不可用，如果该驱动程序不提供相关联的特定于类型请求的回调函数。

该驱动程序时它将调用注册回调函数[ **WdfIoQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuecreate)创建设备的 I/O 队列。

每个回调函数接收两个输入的参数： 的句柄的 I/O 请求的框架将传递到驱动程序和句柄的 I/O 队列的保存请求。 回调函数可以确定目标设备，通过调用[ **WdfIoQueueGetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuegetdevice)。

框架在任意线程上下文中调用您的驱动程序请求处理程序。 驱动程序不应等待时间，并且在任意线程上下文中执行长时间。 在某些情况下，您的驱动程序可能使用内核调度程序对象作为同步机制。 当您的驱动程序可以等待调度程序对象，以及要时它不能执行的操作有关的信息，请参阅[内核调度程序对象简介](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-kernel-dispatcher-objects)。

 

 





