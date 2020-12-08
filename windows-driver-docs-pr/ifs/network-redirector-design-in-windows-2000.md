---
title: Windows 2000 中的网络重定向程序设计
description: Windows 2000 中的网络重定向程序设计
keywords:
- 网络重定向 WDK，Windows 2000
- 重定向程序驱动程序 WDK，Windows 2000
- 重定向驱动器缓冲子系统 WDK 文件系统、Windows 2000
- RDBSS WDK 文件系统，Windows 2000
- 缓冲代码 WDK 网络重定向器
- 内核网络重定向 WDK，Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7566d5134b08fe2b069b52634a9a980ab316abb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832704"
---
# <a name="network-redirector-design-in-windows-2000"></a>Windows 2000 中的网络重定向程序设计


## <span id="ddk_network_redirector_design_in_windows_2000_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_IN_WINDOWS_2000_IF"></span>


网络重定向程序设计中的一项重大挑战是，对于操作选择和计时，从用户启动的操作到低级别网络操作执行的相对比较复杂。 处理 Windows i/o 系统、缓存管理器和内存管理器是一个相对复杂的任务。 在考虑可能适用于远程通信机制的各种缓冲模式（如计算机网络，速度和可靠性可能差别很大）时尤其如此。 网络重定向程序中的这些缓冲操作的实现是一项非常重要的功能，这些投资最好由驱动程序共享和重复使用。

Windows 2000 引入了新的驱动程序模型， (通常称为最小重定向器体系结构，或基于分层或微型端口驱动程序方法的网络重定向器的 rdr2) 。 不需要重新实现用于缓冲和与每个驱动程序中的 i/o 管理器和缓存管理器进行交互的复杂代码，而是将此大代码块提取出来，并将其提供给所有潜在的网络重定向程序。 共享公用缓冲代码称为重定向的驱动器缓冲子系统 (RDBSS) 。

此体系结构具有多个重定向器的模型如下所示。

![说明 windows 2000 中的网络重定向程序设计的示意图](images/redir-02.png)

此 RDBSS 设计更改提供了以下几个优点：

-   简化了为网络重定向程序编写内核驱动程序的过程，因为提供了处理 i/o 系统、缓存管理器和内存管理器所需的大量通用代码。

-   根据为 Microsoft 网络开发的缓冲算法和内核优化，对其他网络重定向程序驱动程序提供了相当多的性能改进。

-   简化维护，因为只需开发和维护一个缓冲代码副本。 在旧模型中，每个重定向程序都需要一个副本。

-   提供网络重定向器的网络协议特定组件的强封装，因此驱动程序开发人员可以将重点放在网络重定向程序的各个方面，这些方面是唯一的，特定于其应用程序或产品。

-   通过基于此分层方法提供分离，简化网络重定向程序的调试驱动程序。

Windows 2000 中引入了 RDBSS 模型。 此同一模型还用于 Windows Server 2003 和 Windows XP。

 

 




