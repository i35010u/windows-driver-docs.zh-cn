---
title: 网络驱动程序编程注意事项
description: 网络驱动程序编程注意事项
keywords:
- 网络驱动程序 WDK，编程注意事项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 883ac255fb1593b6a439413513378b8731f11f59
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840895"
---
# <a name="network-driver-programming-considerations"></a>网络驱动程序编程注意事项





Microsoft Windows 网络驱动程序共享类似的设计目标。 应将网络驱动程序编写为可移植和可伸缩，以便提供硬件和软件的简单配置，使用基于对象的接口，并支持异步 i/o。 本部分介绍如何将这些常规设计目标应用到为 Microsoft Windows Vista 和更高版本的操作系统编写的网络驱动程序。

本节包括下列主题：

-   [网络驱动程序中的性能](performance-in-network-drivers.md)
-   [网络适配器中的性能](performance-in-network-adapters.md)
-   [网络驱动程序中的可移植性](portability-in-network-drivers.md)
-   [网络驱动程序中的多处理器支持](multiprocessor-support-in-network-drivers.md)
-   [网络驱动程序中的 IRQL](irqls-in-network-drivers.md)
-   [网络驱动程序中的同步和通知](synchronization-and-notification-in-network-drivers.md)
-   [网络驱动程序中的数据包结构](packet-structures-in-network-drivers.md)
-   [使用网络驱动程序中的共享内存](using-shared-memory-in-network-drivers.md)
-   [网络驱动程序中的异步 I/O 和 Completion 函数](asynchronous-i-o-and-completion-functions-in-network-drivers.md)
-   [网络驱动程序的安全问题](security-issues-for-network-drivers.md)

 

 





