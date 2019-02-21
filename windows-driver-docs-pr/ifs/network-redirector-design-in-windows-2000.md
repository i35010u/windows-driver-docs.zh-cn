---
title: 在 Windows 2000 中的网络重定向程序设计
description: 在 Windows 2000 中的网络重定向程序设计
ms.assetid: d5a78712-02ee-48f4-86b9-c294b41245a6
keywords:
- 网络重定向程序 WDK，Windows 2000
- 重定向程序驱动程序 WDK，Windows 2000
- 重定向驱动器缓冲子系统 WDK 文件系统中，Windows 2000
- RDBSS WDK 文件系统中，Windows 2000
- 缓冲代码 WDK 网络重定向程序
- 内核网络重定向程序 WDK，Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 318b2c7a8d7507725ffdd7618624186af5cd67ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556081"
---
# <a name="network-redirector-design-in-windows-2000"></a>在 Windows 2000 中的网络重定向程序设计


## <span id="ddk_network_redirector_design_in_windows_2000_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_IN_WINDOWS_2000_IF"></span>


中的网络重定向程序设计的种种难题是相对较复杂从用户启动的操作执行对低级别网络操作，同时操作选择和计时方面的翻译。 处理 Windows I/O 系统时，缓存管理器和内存管理器是一项相对较复杂的任务。 考虑各种缓冲模式可能适用于远程通信机制，例如计算机网络的速度和可靠性可能相差很大时，也是如此。 在网络重定向程序这些缓冲操作的实现表示投入大量的理想情况下将共享和重用由驱动程序的函数。

Windows 2000 引入了新的驱动程序模型 （通常称为最小重定向程序体系结构或 rdr2） 网络重定向程序基于分层或微型端口驱动程序方法。 而不是重新实现复杂的代码用于缓冲和交互使用 I/O 管理器和缓存管理器中每个驱动程序，下面的代码的大块已拉出且可供所有潜在网络重定向程序。 共享公共缓冲的代码称为重定向驱动器缓冲子系统 (RDBSS)。

下面显示了此体系结构与多个重定向程序的模型。

![说明在 windows 2000 中的网络重定向程序设计的关系图](images/redir-02.png)

此 RDBSS 设计更改提供了多个以下优势：

-   简化了大量的常见代码自网络重定向程序写作内核驱动程序的过程所需的 I/O 系统，缓存管理器处理，未提供任何内存管理器。

-   可向其他网络重定向程序驱动程序相当长的基于缓冲算法的性能改进和内核优化 Microsoft 网络的开发。

-   因为只有一份缓冲代码需要进行开发和维护，简化了维护。 在旧模型中，副本所需的每个重定向程序。

-   提供强大的包装的网络协议特定组件的网络重定向器，因此驱动程序开发人员可以专注于为唯一且特定于其应用程序或产品的这些方面的网络重定向程序。

-   通过提供分离基于此分层方法的网络重定向程序简化调试驱动程序。

Windows 2000 引入了 RDBSS 模型。 在 Windows Server 2003 和 Windows XP 还使用此相同的模型。

 

 




