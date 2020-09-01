---
title: 适用于 SAN 的 Windows Sockets SPI 扩展
description: 适用于 SAN 的 Windows Sockets SPI 扩展
ms.assetid: 08f51612-2e2b-439a-8318-43884086828c
keywords:
- SAN 服务提供商 WDK，扩展
- 扩展 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59de6f7b40f751691bf08117037ab28d245d32e0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218282"
---
# <a name="windows-sockets-spi-extensions-for-sans"></a>适用于 SAN 的 Windows Sockets SPI 扩展





本部分提供 SAN 服务提供程序 DLL 必须提供的 SAN 扩展函数的简短说明。 这些函数扩展了用于 SAN 的 Windows 套接 SPI。 扩展函数是在 Ws2san 中定义的，并且在 [Windows 套接 Direct Reference](/previous-versions/windows/hardware/network/ff565857(v=vs.85)) 部分中有完整记录。

除了 **WSPStartupEx** 函数之外，本部分中列出的扩展函数由 Windows 套接交换机检索。 若要检索每个扩展函数的入口点，Windows 套接字开关将调用 SAN 服务提供程序的 [**WSPIoctl**](/previous-versions/windows/hardware/network/ff566296(v=vs.85)) 函数，并传递 SIO \_ 获取 \_ 扩展 \_ 函数 \_ 指针命令代码以及其值标识这些扩展函数之一的 GUID。

SAN 服务提供程序必须实现以下所有扩展函数，但 **WSPRdmaRead** 和 **WSPMemoryRegistrationCacheCallback** 函数除外。 如果 SAN 服务提供程序不支持**WSPRdmaRead**或**WSPMemoryRegistrationCacheCallback**扩展函数，则在 Windows 套接交换机向**WSPRdmaRead**或**WSPMemoryRegistrationCacheCallback**请求入口点时，其**WSPIoctl**函数必须返回错误 WSAEOPNOTSUPP。

<a href="" id="wspstartupex"></a>[**WSPStartupEx**](/previous-versions/windows/hardware/network/ff566321(v=vs.85))  
启动 Windows 套接字交换机对 SAN 服务提供程序的使用。

<a href="" id="wspregistermemory"></a>[**WSPRegisterMemory**](/previous-versions/windows/hardware/network/ff566311(v=vs.85))  
将套接字使用的缓冲数组注册为数据传输操作的本地源或本地目标。 此类套接字可将此缓冲区数组用作 **WSPRdmaWrite** 和 **WSPSend** 调用中的源缓冲区，以及 **WSPRdmaRead** 和 **WSPRecv** 调用中的接收缓冲区。

<a href="" id="wspderegistermemory"></a>[**WSPDeregisterMemory**](/previous-versions/windows/hardware/network/ff566279(v=vs.85))  
释放先前对 **WSPRegisterMemory** 函数的调用注册的缓冲区数组。

<a href="" id="wspregisterrdmamemory"></a>[**WSPRegisterRdmaMemory**](/previous-versions/windows/hardware/network/ff566313(v=vs.85))  
注册向远程对等连接公开的 RDMA 缓冲区数组，以便将数据传输到该对等连接或从该对等连接进行传输。 远程对等节点上的套接字可以使用此 RDMA 缓冲区数组作为 **WSPRdmaWrite** 调用中的目标缓冲区，并使用 **WSPRdmaRead** 调用中的源缓冲区。

<a href="" id="wspderegisterrdmamemory"></a>[**WSPDeregisterRdmaMemory**](/previous-versions/windows/hardware/network/ff566281(v=vs.85))  
释放先前对 **WSPRegisterRdmaMemory** 函数的调用注册的缓冲区数组。

<a href="" id="--------wspmemoryregistrationcachecallback"></a>[**WSPMemoryRegistrationCacheCallback**](/previous-versions/windows/hardware/network/ff566299(v=vs.85))  
释放应用程序缓冲区的所有权和缓冲区与物理内存之间的锁，并从 san 服务提供商的缓存和 SAN NIC 的缓冲区注册中删除该缓冲区。

<a href="" id="wsprdmaread"></a>[**WSPRdmaRead**](/previous-versions/windows/hardware/network/ff566304(v=vs.85))  
将数据从 RDMA 缓冲区传输到地址空间中套接字的远程对等方可以访问的地址空间中的缓冲区。

<a href="" id="wsprdmawrite"></a>[**WSPRdmaWrite**](/previous-versions/windows/hardware/network/ff566306(v=vs.85))  
将源缓冲区中的数据传输到在套接字的远程对等方可以访问的地址空间中，本地套接字可访问目标 RDMA 缓冲区的地址空间中的数据。

 

