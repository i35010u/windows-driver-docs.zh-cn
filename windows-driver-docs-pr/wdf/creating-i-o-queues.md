---
title: 创建 I/O 队列
description: 创建 I/O 队列
ms.assetid: 03b09c94-6b72-4234-b21f-203f93b7a2e8
keywords:
- I/O 队列 WDK KMDF，创建
- I/O 队列 WDK KMDF，默认值
- 默认 I/O 队列 WDK KMDF
- 创建 I/O 队列 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 679be0780c0564f58c23797846cb73f59a074a1d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382369"
---
# <a name="creating-io-queues"></a>创建 I/O 队列





大多数驱动程序创建中的 I/O 队列及其[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。 若要创建设备的 I/O 队列，该驱动程序调用 framework 队列对象的[ **WdfIoQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuecreate)方法 （这会创建 framework 队列对象）。 驱动程序提供[ **WDF\_IO\_队列\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/ns-wdfio-_wdf_io_queue_config)到方法的结构。 此结构包含有关等队列的队列的配置信息[调度方法](dispatching-methods-for-i-o-requests.md)和指向[请求处理程序](request-handlers.md)框架中有请求时调用队列中。 结构还指示队列是否将是[电源管理](using-power-managed-i-o-queues.md)以及是否驱动程序支持长度为零的缓冲区的队列的 I/O 请求。

如果驱动程序设置**DefaultQueue**的成员[ **WDF\_IO\_队列\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/ns-wdfio-_wdf_io_queue_config)结构**TRUE**，该队列变为设备*默认 I/O 队列*。 如果您的驱动程序创建默认 I/O 队列，该框架放置的所有设备的 I/O 请求在此队列，除非创建更多的队列接收的某些请求。 驱动程序可以通过调用获取到设备的默认 I/O 队列句柄[ **WdfDeviceGetDefaultQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdefaultqueue)方法。

如果你想要使用设备的多个 I/O 队列，该驱动程序可以调用[ **WdfIoQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuecreate)创建，如您可以根据需要很多队列对象。 如果驱动程序创建多个队列，它可以调用[ **WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)，它指示框架，以指示不同类型的请求到不同的队列。 例如，您可以指定所有读取请求将传递到一个队列和所有写入请求将传送到另一个队列。

如果您的驱动程序将创建一系列的 I/O 队列并调用[ **WdfDeviceConfigureRequestDispatching** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)若要指示您的驱动程序可以接收到特定队列的请求的每种类型，该驱动程序不需要默认队列。

如果驱动程序不提供针对特定类型的请求的 I/O 队列，并且如果您的驱动程序功能驱动程序，由框架完成请求该类型的状态将完成 status 值\_无效\_设备\_请求。 如果您的驱动程序是一个筛选器驱动程序，并已调用[ **WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitsetfilter)，框架会自动将驱动程序堆栈中的下一步低驱动程序对这些请求转发。 因此，例如，不会处理筛选器驱动程序读取的请求不需要提供接收的 I/O 队列的读取请求。

有关驱动程序如何使用 I/O 队列的示例，请参阅[I/O 队列的示例使用](example-uses-of-i-o-queues.md)。

 

 





