---
title: 为 SAN 上的操作注册内存
description: 为 SAN 上的操作注册内存
ms.assetid: 5492466e-4765-4d43-b6bc-1d5bc74996ba
keywords:
- SAN 连接安装 WDK，注册内存
- 注册内存 San
- 数据缓冲 WDK San
- 缓冲区 WDK San
- 注册数据缓冲区
- 内存 WDK San
- 已注册的内存 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bc6a51cde8a8cb5cd7369a8a0c045f3aa8325dc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373858"
---
# <a name="registering-memory-for-operations-on-a-san"></a>为 SAN 上的操作注册内存





Windows 套接字切换 SAN 服务提供商的扩展函数来注册所有数据缓冲区发送和接收消息和系统区域网络上的 RDMA 操作的调用。 这些扩展函数注册到区域的物理内存的已连接到远程对等方特定 SAN 套接字上使用的缓冲区。 有关这些扩展函数的说明，请参阅[Windows 套接字的 SPI 扩展 San](windows-sockets-spi-extensions-for-sans.md)。

### <a name="registering-data-buffers"></a>注册数据缓冲区

此开关调用 SAN 服务提供商[ **WSPRegisterMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566311)代表注册只能由，可以访问的数据缓冲区的本地进程中运行的应用程序的扩展函数过程。 缓冲区会处理这一切**WSPRegisterMemory**返回是仅在执行注册本地进程的上下文中有效。 交换机调用**WSPRegisterMemory**注册充当消息对的调用中接收缓冲区的缓冲区[ **WSPRecv** ](https://msdn.microsoft.com/library/windows/hardware/ff566309)函数或消息发送缓冲区调用[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)函数。 开关也会调用**WSPRegisterMemory**注册用作对的调用中的本地接收 RDMA 缓冲区的缓冲区[ **WSPRdmaRead** ](https://msdn.microsoft.com/library/windows/hardware/ff566304)扩展函数或在调用本地 RDMA 源[ **WSPRdmaWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff566306)扩展函数。 使用缓冲区注册本地进程完成后**WSPRegisterMemory**，切换调用[ **WSPDeregisterMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566279)到扩展函数释放这些缓冲区。

此开关调用 SAN 服务提供商[ **WSPRegisterRdmaMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566313)代表注册 RDMA 的本地进程中运行的应用程序的扩展函数缓冲的本地和远程进程可以访问。 缓冲描述符的**WSPRegisterRdmaMemory**返回有效值仅为远程对等方启动与 SAN 套接字的已注册的对等节点的连接的上下文中的 RDMA 的数据传输操作执行。 在远程对等连接切换为在调用目标使用这些 RDMA 缓冲区**WSPRdmaWrite**扩展函数或调用中的源**WSPRdmaRead**扩展函数。 使用已注册的缓冲区的本地和远程进程完成后**WSPRegisterRdmaMemory**，切换调用[ **WSPDeregisterRdmaMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566281)扩展函数，以释放这些缓冲区。

### <a name="managing-memory-access"></a>管理内存的访问

SAN 服务提供商必须防止未经授权的访问注册的内存。

内存必须是已注册且可访问，如下所示：

为本地访问应仅供此开关调用的过程注册内存**WSPRegisterMemory**。

为本地和远程访问可以访问由该交换机名为的进程注册内存**WSPRegisterRdmaMemory**注册内存，或由连接到 SAN 的远程对等方套接字到的内存已注册。

仅在注册时和建立连接时，内存必须可访问。 SAN 服务提供商必须确保，它不会无意中使此类内存运行在 SAN 上的同一台计算机上或其他计算机上的其他进程可以访问。

仅为读取访问注册的内存不能用于写访问权限。 必须将注册仅进行写访问的内存可用于读访问。

### <a name="using-registered-memory"></a>使用已注册的内存

开关注册每个连接的 TCP 套接字来协商数据传输会话使用的内存的两个几乎相邻的区域。 交换机使用的内存的一个区域来提供包含发送数据时调用 SAN 服务提供商的消息缓冲区**WSPSend**函数。 交换机使用的内存的其他区域发布消息时调用 SAN 服务提供程序的接收数据的缓冲区**WSPRecv**函数。

仅当传输 RDMA 操作中的应用程序数据，该交换机通常注册 RDMA 缓冲区。

切换开关关闭套接字之前，请拨打**WSPDeregisterMemory**或**WSPDeregisterRdmaMemory** SAN 服务提供程序，以释放任何内存都将挂起的数据传输的函数当前未使用操作。 SAN 服务提供程序还必须释放与未处理的数据传输操作关联的内存。

 

 





