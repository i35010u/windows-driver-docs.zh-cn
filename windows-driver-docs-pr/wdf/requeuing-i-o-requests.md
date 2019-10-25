---
title: 将 I/O 请求重新排队
description: 将 I/O 请求重新排队
ms.assetid: b509959c-b2ab-4f04-9c08-5c5e90726b73
keywords:
- I/o 请求 WDK KMDF，正在重新排队
- 正在重新排队 i/o 请求 WDK KMDF
- 请求处理 WDK KMDF，正在重新排队 i/o 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bb0fa03d0925faa5fa066d3ed05787926b42755
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842223"
---
# <a name="requeuing-io-requests"></a>将 I/O 请求重新排队





驱动程序可以重新排队 i/o 队列中获得的 i/o 请求。 驱动程序可以将 i/o 请求重新排队到驱动程序为同一设备创建的另一 i/o 队列。 此外，[总线驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)还可以将子设备的 i/o 队列中的 i/o 请求重新排队为父设备的 i/o 队列。

### <a name="requeuing-an-io-request-to-a-different-io-queue-for-a-device"></a>向设备的不同 i/o 队列正在重新排队 i/o 请求

驱动程序的请求处理程序从驱动程序的 i/o 队列接收到 i/o 请求后，该驱动程序可以调用[**WdfRequestForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)将请求重新排队到另一个队列。

例如，如果你希望驱动程序在处理请求之前将资源分配给请求，则驱动程序的[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)回调函数可以接收所有请求，在每个请求的上下文内存中存储资源信息，然后调用[**WdfRequestForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)重新排队每个请求添加到另一个队列。

如果你的驱动程序调用[**WdfRequestForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)来重新排队某个 i/o 请求，该驱动程序是从使用顺序[调度方法](dispatching-methods-for-i-o-requests.md)的 i/o 队列获取的，则该框架会将下一个 i/o 请求从顺序队列传递到驱动程序，而无需等待重新排队的请求完成。

如果驱动程序使用手动调度方法，则它可以调用[**WdfRequestRequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestrequeue)方法，将 i/o 请求返回到从中获取驱动程序的 i/o 队列的开头。 调用**WdfRequestRequeue**之后，驱动程序的下一次调用[**WdfIoQueueRetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievenextrequest)会检索重新排队的请求。

### <a name="requeuing-an-io-request-to-a-parent-devices-io-queue"></a>正在重新排队对父设备的 i/o 队列发出 i/o 请求

父设备的函数驱动程序可以充当[枚举](enumerating-the-devices-on-a-bus.md)父设备的子设备的[总线驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)，并为子设备创建[物理设备对象](wdm-concepts-for-kmdf-drivers.md#device-stacks)（PDOs）。 此类驱动程序有时可能会收到父设备必须处理的子设备的 i/o 请求。

例如，协议总线（如 USB）通常控制分配给每个连接的设备的硬件资源。 因此，父总线的函数驱动程序通常会处理每个子设备的 i/o 操作。 当 i/o 管理器将 i/o 请求发送到其中一个子设备的[设备堆栈](wdm-concepts-for-kmdf-drivers.md#device-stacks)时，该总线的函数驱动程序将接收子设备的一个 i/o 队列中的 i/o 请求，因为该驱动程序创建了子设备的 PDO。 在驱动程序可以在父总线设备的上下文中处理 i/o 请求之前，它必须将子设备的 i/o 队列中的 i/o 请求重新排队为属于父设备的 i/o 队列。

但是，驱动程序无法调用[**WdfRequestForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)将请求从子队列移动到父队列。 因为 i/o 管理器为父设备和子设备创建了单独的设备堆栈，所以必须首先将基础 WDM 设备对象从代表子设备的一个对象更改为表示父设备的对象。

在 KMDF 版本1.9 之前，驱动程序只能通过创建[远程 i/o 目标](general-i-o-targets.md)、增加子设备的设备堆栈的大小并指定正确的 WDM 设备对象，将从子设备发送到其父设备的 i/o 请求。

从 KMDF 版本1.9 开始，驱动程序可以先调用[**WdfPdoInitAllowForwardingRequestToParent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent) ，然后再创建子设备，然后调用[**WdfRequestForwardToParentDeviceIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoparentdeviceioqueue) ，重新排队从子 i/o 队列到父队列的请求使. 如果驱动程序使用**WdfPdoInitAllowForwardingRequestToParent**和**WdfRequestForwardToParentDeviceIoQueue**，则框架将增加子的设备堆栈大小，并将正确的 WDM 设备对象分配给 i/o 请求。

 

 





