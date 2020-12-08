---
title: 驱动程序线程上下文
description: 驱动程序线程上下文
keywords:
- 驱动程序线程上下文 WDK 内核
- 线程上下文 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc90ca159030d43459876f6e1ca3f1d511d7475c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825893"
---
# <a name="driver-thread-context"></a>驱动程序线程上下文





如 [处理分层驱动程序中的 irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg) 图所示，文件系统是由两部分构成的驱动程序：

1.  文件系统驱动程序 (FSD) ，它在调用 i/o 系统服务的用户模式线程的上下文中执行

    I/o 管理器将相应的 IRP 发送到 FSD。 如果 FSD 为 IRP 设置完成例程，则不一定会在原始用户模式线程的上下文中调用其完成例程。

2.  一组文件系统线程，可能是 *FSP (文件系统进程)*

    FSD 可以创建一组由驱动程序专用的系统线程，但大多数 FSDs 使用系统工作线程来完成工作，而无需占用发出 i/o 请求的用户模式线程。 任何 FSD 都可以设置自己的进程地址空间，在该空间中，其驱动程序专用线程执行，但系统提供的 FSDs 避免这种做法来节省系统内存。

文件系统通常使用系统工作线程来设置和管理其发送到一个或多个低级驱动程序（可能适用于不同设备）的 Irp 的内部工作队列。

虽然 [分层驱动程序中的处理 irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg) 中所示的最低级别驱动程序会通过一组独立的驱动程序提供的例程来处理每个 IRP，但它不使用系统线程作为文件系统。 最低级别的驱动程序不需要其自己的线程上下文，除非为 i/o 设置其设备是长时间的进程，这会对系统性能产生显著影响。 较低级别或中间的驱动程序需要设置自己的驱动程序专用或专用于设备的系统线程，而那些确实会导致上下文切换到线程的性能损失。

大多数内核模式驱动程序（如 [层次驱动程序中处理 irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg) 中的物理设备驱动程序）都在任意线程上下文中执行：调用以处理 IRP 时，任何线程都是最新的。 因此，驱动程序通常会在其设备对象的驱动程序定义部分（称为 *设备扩展*）中维护有关其 i/o 操作和设备所服务的设备的状态。

 

 




