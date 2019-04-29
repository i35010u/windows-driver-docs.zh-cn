---
title: 驱动程序线程上下文
description: 驱动程序线程上下文
ms.assetid: 8795811d-a5f6-4f90-9fa0-edd4b37fd269
keywords:
- 驱动程序线程上下文 WDK 内核
- 线程上下文 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47b0ec4fe390120559a2e76ddf70c1c93167f25d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372678"
---
# <a name="driver-thread-context"></a>驱动程序线程上下文





如中所示[分层驱动程序中处理 Irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)图，文件系统是由两部分驱动程序：

1.  文件系统驱动程序 (FSD)，可以调用 I/O 系统服务的用户模式线程的上下文中执行

    I/O 管理器将相应的 IRP 发送到 FSD。 如果为 IRP，FSD 设置完成例程，其完成例程不一定是原始用户模式线程的上下文中调用。

2.  设置的文件系统线程和可能是一个*FSP （文件系统进程）*

    FSD 可以创建一组驱动程序专用系统线程，但大多数 FSDs 使用以获取无需占用发出 I/O 请求的用户模式线程完成工作的系统工作线程数。 任何 FSD 可能设置了其自己的进程地址空间，其驱动程序专用的线程执行，但系统提供 FSDs 避免这种做法，以节省系统内存。

文件系统通常使用系统工作线程数来设置和管理其发送到一个或多个较低级别设备的驱动程序，可能是不同的 Irp 的内部工作队列。

尽管最低级别的驱动程序中所示[分层驱动程序中处理 Irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)图通过一系列离散、 驱动程序所提供的例程的阶段中处理每个 IRP，它不使用系统线程，文件系统一样。 最低级别驱动程序不需要其自己的线程上下文，除非其设备设置为 I/O 是这样的较长时间的进程，它具有系统性能产生明显的影响。 几个最低级别或中间驱动程序需要设置其自己的驱动程序专用或设备专用系统线程，以及需要付费引起的上下文切换到其线程对性能产生负面影响。

大多数内核模式驱动程序等中的物理设备驱动程序[分层驱动程序中处理 Irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)图，请在任意线程上下文中执行： 的任何线程恰巧是当前按调用来处理 IRP。 因此，驱动程序通常会维护有关它们的 I/O 操作和在处理其设备对象，称为驱动程序定义部分中的设备的状态*设备扩展*。

 

 




