---
title: 驱动程序管理的 IRP 队列
description: 驱动程序管理的 IRP 队列
ms.assetid: b701e4aa-96ba-44af-96a5-b6cecf075bac
keywords:
- 设备队列 WDK Irp，对象
- Irp WDK 内核队列
- 队列的 Irp
- 取消排队的 Irp
- 内部 IRP 队列 WDK 内核
- 取消安全 IRP 队列 WDK 内核
- 驱动程序管理 IRP 队列 WDK 内核
- 补充 IRP 队列 WDK 内核
- 互锁的 IRP 队列 WDK 内核
- 设备队列 WDK Irp
- 设备队列 WDK Irp，有关设备队列
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9ebe8a4e657ff53dd6456bdfa98266798a687e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355725"
---
# <a name="driver-managed-irp-queues"></a>驱动程序管理的 IRP 队列





除了文件系统驱动程序，I/O 管理器将设备队列对象 （适用于队列 Irp) 与每个驱动程序创建的设备对象相关联。

若要使用关联的设备队列，其中包含 Irp，设备 I/O 请求的目标设备对象时的 I/O 管理器的支持例程比该驱动程序更快地进入的大多数设备驱动程序调用可处理这些完成。 使用此技术，Irp 排队到驱动程序提供[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程。

为了提高性能，大多数中间驱动程序只需通过 Irp 到低级驱动程序快速客户来了，因此中间驱动程序几乎不会使用其各自的设备对象与关联的设备队列。

但是，您可以设计一个驱动程序以通过显式设置一个或多个设备队列、 互锁的队列或取消安全队列管理的 Irp 的内部队列。 这种方法可以是驱动程序控制的设备，重叠 I/O 操作的情况特别有用。 对于此类设备，它可能很难管理的同一目标设备对象使用单个队列的两个或多个 Irp 的并发处理。

构建内部队列的最简单方法是使用取消安全 IRP 队列框架。 您可以在您的驱动程序中实现所选的排队机制。 然后，可以使用[ **IoCsqInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff549054)注册的一组处理 IRP 插入和删除操作，以及锁定和解锁您的队列的回调例程。 取消安全 IRP 队列框架提供了[ **IoCsqInsertIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549066)， [ **IoCsqRemoveIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549070)，和[ **IoCsqRemoveNextIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549072)自动使用回调例程可以安全地插入和删除驱动程序的队列中的 Irp 的例程。 系统还使用回调例程来安全地删除任何 Irp 中被取消。

您还可能选择为 Irp 的补充队列设置中的一组异类物理设备的设备控制器的驱动程序。 例如，SCSI 端口驱动程序使用设备队列对象的内部队列。 此驱动程序这两个具有*StartIo*例程和设备设置队列的对象作为补充的队列，它创建表示 HBA 除了设备对象与关联的设备队列。 SCSI 端口驱动程序使用其补充设备队列来保存 Irp，特定的逻辑单元绑定 HBA 控制 SCSI bus(es) 上。

系统软盘控制器驱动程序是不具有的驱动程序的示例*StartIo*例程，并使用互锁的队列。 此驱动程序设置在其中和从中驱动程序和其设备专用线程插入和移除 Irp 双向链接的联锁队列。

内核定义设备队列对象类型。 执行支持组件提供了用于插入和删除 Irp 互锁队列中的例程。 Windows XP 和更高版本的 Windows 驱动程序可以使用[取消安全 IRP 队列](cancel-safe-irp-queues.md)处理 IRP 队列。

以下各节说明如何使用设备队列、 互锁的队列和取消安全队列：

[设置和使用设备队列](setting-up-and-using-device-queues.md)

[管理设备队列](managing-device-queues.md)

[设置和使用互锁的队列](setting-up-and-using-interlocked-queues.md)

[管理互锁与驱动程序创建线程队列](managing-interlocked-queues-with-a-driver-created-thread.md)

[取消安全 IRP 队列](cancel-safe-irp-queues.md)

 

 




