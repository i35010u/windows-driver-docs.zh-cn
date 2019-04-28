---
title: RDBSS 驱动程序和库
description: RDBSS 驱动程序和库
ms.assetid: fb2d1939-7af5-474c-8247-e5d48b4bbed6
keywords:
- 网络重定向程序 WDK，RDBSS
- 重定向程序驱动程序 WDK RDBSS
- 内核网络重定向程序 WDK RDBSS
- RDBSS WDK 的文件系统
- 文件系统驱动程序 WDK，RDBSS
- 静态库 WDK 文件系统
- 有关 RDBSS RDBSS WDK 文件系统
- 重定向驱动器缓冲子系统 WDK 的文件系统，有关 RDBSS
- 最小-重定向程序 WDK RDBSS
- 结构 WDK RDBSS
- 数据结构 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49cda6750c52393893d524dc2ae72676de60bc33
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352184"
---
# <a name="the-rdbss-driver-and-library"></a>RDBSS 驱动程序和库


## <span id="ddk_the_rdbss_driver_and_library_if"></span><span id="DDK_THE_RDBSS_DRIVER_AND_LIBRARY_IF"></span>


在两个窗体中实现重定向驱动器缓冲子系统 (RDBSS):

-   文件系统驱动程序 (*rdbss.sys*) 随操作系统一起提供。

-   静态库 (*rdbsslib.lib*) 提供与 Windows Driver Kit (WDK)。

*Rdbss.sys*如果系统上注册了任何非整体化网络微型-重定向程序自动加载驱动程序。 Microsoft 服务器消息块 (SMB) 重定向程序 (*mrxsmb sys*) 是目前唯一可以生成为一个非单一式网络最小化重定向程序驱动程序的驱动因素。

所有其他网络微型重定向程序驱动程序，包括其他 Microsoft 网络微型-重定向程序随操作系统一起提供，必须作为整体化与链接的驱动程序实现*rdbsslib.lib*静态库提供使用 WDK。

RDBSS 使用定义完善的机制来与网络微型重定向程序驱动程序、 I/O 管理器、 缓存管理器中，内存管理器和其他内核系统通信。

RDBSS 导出大量可由网络微型重定向和其他内核系统，设置选项并执行各种操作调用的例程。 若要调用由 RDBSS 导出的例程，网络微型重定向程序驱动程序 （或其他内核驱动程序） 包括相应的 WDK 标头文件，调用导出的 RDBSS 例程的名称，并使用相应链接*rdbsslib.lib*文件随 WDK 一起安装。 请注意，不同*rdbsslib.lib*文件提供了 WDK 用于 Window Vista、 Windows Server 2003、 Windows XP 和 Windows 2000。

RDBSS WDK 的标头文件还定义了若干个建议用于通过网络微型重定向程序驱动程序，而不是直接调用的一些 RDBSS 例程的宏。

由 RDBSS 定义和使用的数据结构的所有在验证中广泛使用的数据结构的开头带有一个特殊 4 字节的签名。 在 WDK 标头文件中，定义这些 RDBSS 数据结构签名的值*nodetype.h*。 这些数据结构签名用于故障排除和调试 RDBSS 和网络微型重定向程序驱动程序。

以下各节讨论中的详细信息每个类别的例程由 RDBSS 导出和定义来调用这些例程的宏。 我们开始使用所有 RDBSS 和类似 RDBSS 所定义的宏的列表提供的例程的列表：

-   [提供的 RDBSS 例程](routines-provided-by-rdbss.md)

-   [定义由 RDBSS 宏](macros-defined-by-rdbss.md)

导出的 RDBSS 和定义来调用这些例程的 RDBSS 宏的例程可以组织成数量的不同类别，其中包括：

-   [驱动程序注册和启动/停止控件](driver-registration-and-start-stop-control.md)

-   [池分配和免费的例程](pool-allocation-and-free-routines.md)

-   [计时器和工作线程管理](timer-and-worker-thread-management.md)

-   [调度机制的工作队列](work-queue-dispatching-mechanisms.md)

-   [诊断和调试](diagnostics-and-debugging.md)

-   [日志记录例程和宏](logging-routines-and-macros.md)

-   [杂项例程](miscellaneous-routines2.md)

-   [RX\_上下文和 IRP 管理](rx-context-and-irp-management.md)

-   [连接和文件结构管理](connection-and-file-structure-management.md)

-   [FCB 资源同步](fcb-resource-synchronization.md)

-   [缓冲状态的控件](buffering-state-control.md)

-   [低 I/O 例程](low-i-o-routines.md)

-   [名称缓存管理](name-cache-management.md)

-   [前缀表管理](prefix-table-management.md)

-   [清除和清理控件](purging-and-scavenging-control.md)

-   [多路复用 ID 管理](multiplex-id-management.md)

-   [引擎的连接管理](connection-engine-management.md)

 

 




