---
title: 创建 I/O 队列
description: 创建 I/O 队列
ms.assetid: 03b09c94-6b72-4234-b21f-203f93b7a2e8
keywords:
- I/o 队列 WDK KMDF，创建
- I/o 队列 WDK KMDF，默认值
- 默认 i/o 队列 WDK KMDF
- 创建 i/o 队列 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dd5b886ff3c3881a16c3eaedc92a217467c8eb7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841761"
---
# <a name="creating-io-queues"></a>创建 I/O 队列





大多数驱动程序在其[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数中创建 i/o 队列。 若要为设备创建 i/o 队列，驱动程序将调用框架队列对象的[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)方法（该方法创建框架队列对象）。 驱动程序向方法提供[**WDF\_IO\_队列\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)结构。 此结构包含有关队列的配置信息，例如队列的[调度方法](dispatching-methods-for-i-o-requests.md)和指针，指向当请求在队列中可用时框架调用的[请求处理程序](request-handlers.md)。 该结构还指示是否将对队列进行[电源管理](using-power-managed-i-o-queues.md)以及驱动程序是否支持队列的 i/o 请求的长度为零的缓冲区。

如果驱动程序将[**WDF\_IO\_QUEUE\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)结构中的**DefaultQueue**成员设置为**TRUE**，则队列将成为设备的*默认 i/o 队列*。 如果你的驱动程序创建默认 i/o 队列，则框架将所有设备的 i/o 请求都放入此队列中，除非你创建其他队列来接收某些请求。 驱动程序可以通过调用[**WdfDeviceGetDefaultQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdefaultqueue)方法来获取设备的默认 i/o 队列的句柄。

如果要对某个设备使用多个 i/o 队列，则驱动程序可以调用[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)来创建所需数量的队列对象。 如果驱动程序创建多个队列，则它可以调用[**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)，这会指示框架将不同类型的请求定向到不同的队列。 例如，你可以指定将所有读取请求传递到一个队列，并将所有写入请求发送到另一个队列。

如果你的驱动程序创建一组 i/o 队列，并调用[**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)来指示你的驱动程序可以接收到特定队列的每种类型的请求，则该驱动程序不需要默认队列。

如果驱动程序没有为特定类型的请求提供 i/o 队列，并且你的驱动程序是函数驱动程序，则框架将完成该类型的请求，其完成状态值为 "状态\_无效\_设备\_请求"。 如果驱动程序是筛选器驱动程序，并且已调用[**WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter)，框架会自动将这些请求转发到驱动程序堆栈中的下一个较低版本的驱动程序。 例如，不处理读取请求的筛选器驱动程序不必提供接收读取请求的 i/o 队列。

有关驱动程序如何使用 i/o 队列的示例，请参阅[I/o 队列的示例用法](example-uses-of-i-o-queues.md)。

 

 





