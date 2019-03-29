---
title: 网络驱动程序编程注意事项
description: 网络驱动程序编程注意事项
ms.assetid: 43e97f33-8470-440c-b4f4-78752def2dcf
keywords:
- 网络驱动程序 WDK，编程注意事项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dc4226ba0cc1db8c5e69397a47b2e082d843aa0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568681"
---
# <a name="network-driver-programming-considerations"></a>网络驱动程序编程注意事项





Microsoft Windows 网络驱动程序共享类似的设计目标。 网络驱动程序应编写可移植和可伸缩性，以提供的硬件和软件，来使用基于对象的接口，并支持异步 I/O 的简单配置。 本部分介绍如何将这些常规设计目标应用于编写适用于 Microsoft Windows Vista 和更高版本操作系统的网络驱动程序。

本部分包括以下主题：

-   [中的网络驱动程序的性能](performance-in-network-drivers.md)
-   [中的网络适配器的性能](performance-in-network-adapters.md)
-   [网络驱动程序中的可移植性](portability-in-network-drivers.md)
-   [网络驱动程序中的多处理器支持](multiprocessor-support-in-network-drivers.md)
-   [网络驱动程序中于 Irql](irqls-in-network-drivers.md)
-   [同步和网络驱动程序中的通知](synchronization-and-notification-in-network-drivers.md)
-   [网络驱动程序中的数据包结构](packet-structures-in-network-drivers.md)
-   [使用共享内存中的网络驱动程序](using-shared-memory-in-network-drivers.md)
-   [异步 I/O 和网络驱动程序中的完成函数](asynchronous-i-o-and-completion-functions-in-network-drivers.md)
-   [网络驱动程序的安全问题](security-issues-for-network-drivers.md)

 

 





