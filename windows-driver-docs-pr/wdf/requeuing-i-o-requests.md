---
title: 排队 I/O 请求
description: 排队 I/O 请求
ms.assetid: b509959c-b2ab-4f04-9c08-5c5e90726b73
keywords:
- I/O 请求 WDK KMDF，排队
- 排队 I/O 请求 WDK KMDF
- 请求处理 WDK KMDF 排队 I/O 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7971188e2320f3c9c830be575e14b404e6a5a25a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546324"
---
# <a name="requeuing-io-requests"></a>排队 I/O 请求





驱动程序可以将它们从 I/O 队列中获取的 I/O 请求重新排队。 驱动程序可以将对另一个驱动程序已在同一设备为创建的 I/O 队列的 I/O 请求重新排队。 此外，[总线驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540704)可以对来自子设备的 I/O 队列到父设备的 I/O 队列的 I/O 请求重新排队。

### <a name="requeuing-an-io-request-to-a-different-io-queue-for-a-device"></a>排队 I/O 请求到不同设备的 I/O 队列

该驱动程序的驱动程序请求处理程序从驱动程序的 I/O 队列中接收的 I/O 请求后，可以调用[ **WdfRequestForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549958)以对另一个队列的请求重新排队。

例如，如果希望您的驱动程序将请求的资源分配处理请求，该驱动程序的前[ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)回调函数可以接收所有请求，存储资源每个请求的上下文内存，然后调用中的信息[ **WdfRequestForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549958)若要对其他队列的每个请求重新排队。

如果您的驱动程序调用[ **WdfRequestForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549958)到重新排队 I/O 请求驱动程序从一个 I/O 获取队列的使用顺序[调度方法](dispatching-methods-for-i-o-requests.md)，该框架将提供下一步的 I/O 请求从顺序队列向驱动程序而无需等待完成重新排队请求。

如果您的驱动程序使用手动调度方法，它可以调用[ **WdfRequestRequeue** ](https://msdn.microsoft.com/library/windows/hardware/ff550012)方法以返回到从中驱动程序获取它的 I/O 队列开头的 I/O 请求。 在调用**WdfRequestRequeue**，驱动程序的下一步调用[ **WdfIoQueueRetrieveNextRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548462)检索重新排队的请求。

### <a name="requeuing-an-io-request-to-a-parent-devices-io-queue"></a>排队 I/O 请求到父设备的 I/O 队列

父设备功能驱动程序可充当[总线驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540704)的[枚举](enumerating-the-devices-on-a-bus.md)父设备的子设备，并创建[物理设备对象](wdm-concepts-for-kmdf-drivers.md#device-stacks)(PDOs) 为子设备。 此类驱动程序有时可以接收子设备父设备必须处理的 I/O 请求。

例如，协议总线 （例如 USB) 通常控制分配给每个连接的设备的硬件资源。 因此，父总线功能驱动程序通常会处理每个子设备的 I/O 操作。 当 I/O 管理器发送的 I/O 请求[设备堆栈](wdm-concepts-for-kmdf-drivers.md#device-stacks)的子设备之一，总线功能驱动程序的 I/O 请求之一接收子设备的 I/O 队列，因为该驱动程序创建子设备 PDO。 该驱动程序可以处理 I/O 请求的父总线设备上下文中之前，它必须对来自子设备的 I/O 队列到属于父设备的 I/O 队列的 I/O 请求重新排队。

但是，驱动程序不能调用[ **WdfRequestForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549958)将请求从子队列移动到父级的队列。 由于 I/O 管理器创建单独的设备堆栈的父级和子级的设备，则必须首先从一个子设备表示为一个表示父更改基础 WDM 设备对象。

之前 KMDF 1.9 版中，驱动程序无法输入/输出请求从子设备发送到其父仅通过创建[远程 I/O 目标](general-i-o-targets.md)、 增加子设备的设备堆栈的大小，并指定正确的 WDM 设备对象。

从 KMDF 1.9 版开始，驱动程序可以调用[ **WdfPdoInitAllowForwardingRequestToParent** ](https://msdn.microsoft.com/library/windows/hardware/ff548789)设备，然后调用创建子级之前[ **WdfRequestForwardToParentDeviceIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549959)以对来自子范围的 I/O 队列到父队列的请求重新排队。 如果驱动程序将使用**WdfPdoInitAllowForwardingRequestToParent**并**WdfRequestForwardToParentDeviceIoQueue**，框架会增加子范围的设备堆栈大小，并将分配正确 WDM对 I/O 请求的设备对象。

 

 





