---
title: 线程对象简介
description: 线程对象简介
ms.assetid: c41dd20e-07c1-432f-b012-ecc45fe44413
keywords:
- 线程对象 WDK 内核
- 系统进程线程 WDK 内核
- 设备专用线程 WDK 内核
- 系统工作线程 WDK 内核
- 辅助角色线程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7add3f0b02cff985480270fee864a4f7ad3a3b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567870"
---
# <a name="introduction-to-thread-objects"></a>线程对象简介





用户模式线程对象表示在当前进程中执行的路径。 每个用户模式线程对象是通过使用嵌入的内核模式线程对象实现的。

内核模式线程对象是内核定义调度程序对象类型的实例。 它表示该线程是操作系统中的基本可计划实体。

线程对象：

-   是由内核执行调度。

-   在任意给定时刻具有以下属性：

    -   *调度状态*

    -   *priority*

    -   *context*

    -   执行模式 （内核或用户）

    -   *affinity*

-   "由拥有"将进程对象，但可以将自身附加到另一个进程的地址空间。

通常情况下，大多数驱动程序的上下文中执行的当前运行的线程，即，在任意线程上下文中。 尽管文件系统驱动程序可以创建一个独立过程，用于自己的设备专用线程，文件系统通常避免设置驱动程序创建进程和线程，为了节省系统内存并避免上下文切换的开销。

FSs （和其他驱动程序） 可以设置设备专用 （系统进程） 线程和/或 FSs 可以使用系统工作线程数，如果他们需要在其中执行的特定于驱动程序的线程上下文。 驱动程序使用内核模式**Ps * Xxx*** 例程，从而创建进程和/或设备专用线程。 FSs 调用**Ex * Xxx*** 例程使用系统工作线程数。

 

 




