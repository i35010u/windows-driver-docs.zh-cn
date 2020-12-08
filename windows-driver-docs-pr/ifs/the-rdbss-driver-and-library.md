---
title: RDBSS 驱动程序和库
description: RDBSS 驱动程序和库
keywords:
- 网络重定向 WDK，RDBSS
- 重定向程序驱动程序 WDK，RDBSS
- 内核网络重定向 WDK，RDBSS
- RDBSS WDK 文件系统
- 文件系统驱动程序 WDK，RDBSS
- 静态库 WDK 文件系统
- RDBSS WDK 文件系统，关于 RDBSS
- 重定向驱动器缓冲子系统 WDK 文件系统，关于 RDBSS
- 小型重定向程序 WDK，RDBSS
- 结构 WDK RDBSS
- 数据结构 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: affe7b8a627585df69becef06005fdc74aacb9b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830525"
---
# <a name="the-rdbss-driver-and-library"></a>RDBSS 驱动程序和库


## <span id="ddk_the_rdbss_driver_and_library_if"></span><span id="DDK_THE_RDBSS_DRIVER_AND_LIBRARY_IF"></span>


重定向的驱动器缓冲子系统 (RDBSS) 采用以下两种形式实现：

-   文件系统驱动程序 (随操作系统提供 *rdbss.sys*) 。

-   ) 随 Windows 驱动程序工具包一起提供 (WDK) 的静态库 *(。*

如果在系统上注册了任何非单一网络微型重定向程序，则会自动加载 *rdbss.sys* 驱动程序。 Microsoft 服务器消息块 (SMB) 重定向程序 (*mrxsmb sys*) 目前是唯一可作为非单一网络小型重定向程序驱动程序构建的驱动程序。

所有其他网络微型重定向程序驱动程序（包括随操作系统提供的其他 Microsoft 网络小型重定向器）都必须作为与 WDK 一起提供的 *rdbsslib* 静态库链接的单一驱动程序来实现。

RDBSS 使用明确定义的机制与网络小型重定向程序驱动程序、i/o 管理器、缓存管理器、内存管理器和其他内核系统进行通信。

RDBSS 导出大量例程，这些例程可由网络微型重定向程序和其他内核系统调用以设置选项和执行各种操作。 若要调用 RDBSS 导出的例程，网络微型重定向程序驱动程序 (或其他内核驱动程序) 包括适当的 WDK 标头文件、按名称调用导出的 RDBSS 例程，并使用与 WDK 一起安装的相应 *rdbsslib* 文件的链接。 请注意，随 windows Vista、Windows Server 2003、Windows XP 和 Windows 2000 的 WDK 一起提供了不同的 *rdbsslib 文件。*

RDBSS 的 WDK 标头文件还定义了多个建议用于网络小型重定向程序驱动程序的宏，而不是直接调用某些 RDBSS 例程。

RDBSS 定义并使用的所有数据结构在验证中广泛使用的数据结构的开头有一个特殊的4字节签名。 这些 RDBSS 数据结构签名的值是在 WDK 头文件中定义 *的。* 这些数据结构签名用于排除和调试 RDBSS 和网络小型重定向器驱动程序。

以下各节详细介绍了 RDBSS 导出的每个例程类别以及为调用这些例程定义的宏。 接下来，我们将从 RDBSS 提供的所有例程列表和 RDBSS 定义的类似宏列表开始：

-   [RDBSS 提供的例程](routines-provided-by-rdbss.md)

-   [RDBSS 定义的宏](macros-defined-by-rdbss.md)

RDBSS 导出的例程和定义为调用这些例程的 RDBSS 宏可以组织为多个不同的类别，其中包括：

-   [驱动程序注册和启动/停止控制](driver-registration-and-start-stop-control.md)

-   [池分配和自由例程](pool-allocation-and-free-routines.md)

-   [计时器和工作线程管理](timer-and-worker-thread-management.md)

-   [工作队列调度机制](work-queue-dispatching-mechanisms.md)

-   [诊断和调试](diagnostics-and-debugging.md)

-   [记录例程和宏](logging-routines-and-macros.md)

-   [其他例程](miscellaneous-routines2.md)

-   [RX \_ 上下文和 IRP 管理](rx-context-and-irp-management.md)

-   [连接和文件结构管理](connection-and-file-structure-management.md)

-   [FCB 资源同步](fcb-resource-synchronization.md)

-   [缓冲状态控制](buffering-state-control.md)

-   [低 i/o 例程](low-i-o-routines.md)

-   [名称缓存管理](name-cache-management.md)

-   [前缀表管理](prefix-table-management.md)

-   [清除和清理控件](purging-and-scavenging-control.md)

-   [多路复用 ID 管理](multiplex-id-management.md)

-   [连接引擎管理](connection-engine-management.md)

 

 




