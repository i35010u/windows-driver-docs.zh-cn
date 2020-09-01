---
title: 为 SAN 上的操作注册内存
description: 为 SAN 上的操作注册内存
ms.assetid: 5492466e-4765-4d43-b6bc-1d5bc74996ba
keywords:
- SAN 连接设置 WDK，注册内存
- 为 San 注册内存
- 数据缓冲区 WDK San
- 缓冲 WDK San
- 正在注册数据缓冲区
- 内存 WDK San
- 已注册内存 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4503fe1ae7cf13522978780c42c32976330b8951
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211993"
---
# <a name="registering-memory-for-operations-on-a-san"></a>为 SAN 上的操作注册内存





Windows 套接字交换机调用 SAN 服务提供程序的扩展功能，以注册用于发送和接收消息的所有数据缓冲区，以及用于在系统区域网络上进行 RDMA 操作的所有数据缓冲区。 这些扩展函数将缓冲区注册到物理内存区域，以供连接到远程对等方的特定 SAN 套接字使用。 有关这些扩展函数的说明，请参阅 [适用于 san 的 Windows 套接 SPI 扩展](windows-sockets-spi-extensions-for-sans.md)。

### <a name="registering-data-buffers"></a>正在注册数据缓冲区

开关代表在本地进程中运行的应用程序调用 SAN 服务提供程序的 [**WSPRegisterMemory**](/previous-versions/windows/hardware/network/ff566311(v=vs.85)) extension 函数，以注册只能由该进程访问的数据缓冲区。 缓冲区处理 **WSPRegisterMemory** 返回仅在执行注册的本地进程的上下文中有效。 开关调用 **WSPRegisterMemory** 来注册在对 [**WSPRecv**](/previous-versions/windows/hardware/network/ff566309(v=vs.85)) 函数的调用中充当消息接收缓冲区的缓冲区，或调用对 [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85)) 函数的调用中的消息发送缓冲区。 开关还会调用**WSPRegisterMemory** ，以便在调用[**WSPRdmaWrite**](/previous-versions/windows/hardware/network/ff566306(v=vs.85))扩展函数时，将用作本地接收 rdma 缓冲区的缓冲区注册到[**WSPRDMAREAD**](/previous-versions/windows/hardware/network/ff566304(v=vs.85))扩展函数或本地 RDMA 源。 在本地进程完成使用向 **WSPRegisterMemory**注册的缓冲区后，开关会调用 [**WSPDeregisterMemory**](/previous-versions/windows/hardware/network/ff566279(v=vs.85)) 扩展函数以释放这些缓冲区。

开关代表在本地进程中运行的应用程序调用 SAN 服务提供程序的 [**WSPRegisterRdmaMemory**](/previous-versions/windows/hardware/network/ff566313(v=vs.85)) extension 函数，以注册本地和远程进程都可以访问的 RDMA 缓冲区。 **WSPRegisterRdmaMemory**返回的缓冲区说明符仅对远程对等节点在对等连接到在其上执行注册的 SAN 套接字的连接上下文中启动的 RDMA 数据传输操作有效。 远程对等连接上的开关使用这些 RDMA 缓冲区作为对 **WSPRdmaWrite** 扩展函数或调用 **WSPRdmaRead** 扩展函数的源中的目标。 在本地和远程进程完成使用向 **WSPRegisterRdmaMemory**注册的缓冲区后，开关会调用 [**WSPDeregisterRdmaMemory**](/previous-versions/windows/hardware/network/ff566281(v=vs.85)) 扩展函数以释放这些缓冲区。

### <a name="managing-memory-access"></a>管理内存访问

SAN 服务提供程序必须阻止对已注册内存的未经授权的访问。

必须按如下所示注册和访问内存：

为本地访问注册的内存应仅适用于在其中调用 **WSPRegisterMemory**的进程。

为本地和远程访问注册的内存可以通过调用 **WSPRegisterRdmaMemory** 来注册内存的进程或连接到已注册内存的 SAN 套接字的远程对等方访问。

只有在注册和建立连接时，才能访问内存。 SAN 服务提供程序必须确保在同一台计算机上或在 SAN 上的其他计算机上运行的其他进程不会无意中使此类内存可供访问。

仅为读取访问权限注册的内存不能用于写访问。 仅为写入访问权限注册的内存不能用于读访问。

### <a name="using-registered-memory"></a>使用已注册的内存

开关为每个连接的 TCP 套接字注册两个虚拟连续的内存区域，用于协商数据传输会话。 开关在调用 SAN 服务提供程序的 **WSPSend** 函数时，使用一个内存区域来提供包含发送数据的消息缓冲区。 在调用 SAN 服务提供程序的 **WSPRecv** 函数时，开关使用另一个内存区域来发布消息缓冲区以接收数据。

通常情况下，此开关仅在其传输 RDMA 操作中的应用程序数据时才注册 RDMA 缓冲区。

开关在关闭套接字之前，会调用 SAN 服务提供程序的 **WSPDeregisterMemory** 或 **WSPDeregisterRdmaMemory** 函数，以释放当前未使用的任何内存。 SAN 服务提供程序还必须释放与未完成的数据传输操作相关联的内存。

 

