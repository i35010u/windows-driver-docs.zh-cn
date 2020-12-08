---
title: 线程对象简介
description: 线程对象简介
keywords:
- 线程对象 WDK 内核
- 系统进程线程 WDK 内核
- 设备专用线程 WDK 内核
- 系统工作线程 WDK 内核
- 工作线程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5133aac86e338b34b1c4d0a4a0a2a8bd47007af7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838871"
---
# <a name="introduction-to-thread-objects"></a>线程对象简介





用户模式线程对象表示当前进程中的执行路径。 每个用户模式线程对象都是通过使用嵌入的内核模式线程对象实现的。

内核模式线程对象是内核定义的调度程序对象类型的实例。 它表示的线程是操作系统中的基本可计划实体。

Thread 对象：

-   由内核用于执行。

-   在任意给定时刻都具有以下属性：

    -   *调度状态*

    -   *priority*

    -   *上下文*

    -    (内核或用户的执行模式) 

    -   *性*

-   是一个进程对象，但它可以附加到另一个进程的地址空间。

通常，大多数驱动程序在当前运行的线程的上下文中执行，即任意线程上下文中。 尽管文件系统驱动程序可以为其自己的设备专用线程创建独立的进程，但文件系统通常会避免设置驱动程序创建的进程和线程，以便节省系统内存并避免上下文切换的开销。

) 的 FSs (和其他驱动程序可以设置设备专用 (系统进程) 线程，并且/或 FSs 在需要执行特定于驱动程序的线程上下文时，可以使用系统工作线程。 驱动程序使用内核模式 **Ps * Xxx*** 例程来创建进程和/或设备专用线程。 FSs 调用 **Ex * Xxx*** 例程来使用系统工作线程。

 

 




