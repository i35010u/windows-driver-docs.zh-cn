---
title: 适用于 SAN 的 Windows Sockets SPI 扩展
description: 适用于 SAN 的 Windows Sockets SPI 扩展
ms.assetid: 08f51612-2e2b-439a-8318-43884086828c
keywords:
- SAN 服务提供商 WDK，扩展
- 扩展 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdee038a127e9c5f8c4f716e9a437143002ad7c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353596"
---
# <a name="windows-sockets-spi-extensions-for-sans"></a>适用于 SAN 的 Windows Sockets SPI 扩展





本部分提供 SAN 服务提供程序 DLL 必须提供 SAN 扩展函数的简要说明。 这些函数来扩展 Windows 套接字的 SPI 用于使用 SAN。 扩展的函数在 Ws2san.h 中定义并完全记录在[Windows 套接字直接引用](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565857(v=vs.85))部分。

除**WSPStartupEx**函数，将在本部分中列出的扩展的函数检索通过 Windows 套接字切换。 若要检索每个这些扩展函数的入口点，Windows 套接字开关调用 SAN 服务提供商[ **WSPIoctl** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566296(v=vs.85))函数，并将传递 SIO\_获取\_扩展\_函数\_指针命令代码以及其值标识其中一种 GUID 扩展函数。

SAN 服务提供程序必须实现以下扩展函数之外的所有**WSPRdmaRead**并**WSPMemoryRegistrationCacheCallback**函数。 如果 SAN 服务提供程序不支持任一**WSPRdmaRead**或**WSPMemoryRegistrationCacheCallback**扩展函数，其**WSPIoctl**函数必须返回错误 WSAEOPNOTSUPP 时切换 Windows 套接字请求为入口点**WSPRdmaRead**或**WSPMemoryRegistrationCacheCallback**。

<a href="" id="wspstartupex"></a>[**WSPStartupEx**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566321(v=vs.85))  
启动 Windows 套接字切换的 SAN 服务提供程序的使用。

<a href="" id="wspregistermemory"></a>[**WSPRegisterMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566311(v=vs.85))  
注册一个套接字使用作为本地源或本地的数据传输操作目标的缓冲区数组。 此类套接字可以使用此缓冲区数组作为源缓冲区**WSPRdmaWrite**并**WSPSend**中的调用和接收缓冲区**WSPRdmaRead**和**WSPRecv**调用。

<a href="" id="wspderegistermemory"></a>[**WSPDeregisterMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566279(v=vs.85))  
释放已由以前调用注册的缓冲区数组**WSPRegisterMemory**函数。

<a href="" id="wspregisterrdmamemory"></a>[**WSPRegisterRdmaMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566313(v=vs.85))  
将注册公开相互传输数据从该对等连接的远程对等方连接到 RDMA 缓冲区数组。 在远程对等方的套接字可以使用此 RDMA 缓冲区数组作为目标缓冲区**WSPRdmaWrite**调用，并且源中的缓冲区**WSPRdmaRead**调用。

<a href="" id="wspderegisterrdmamemory"></a>[**WSPDeregisterRdmaMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566281(v=vs.85))  
释放已由以前调用注册的缓冲区数组**WSPRegisterRdmaMemory**函数。

<a href="" id="--------wspmemoryregistrationcachecallback"></a>[**WSPMemoryRegistrationCacheCallback**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566299(v=vs.85))  
释放应用程序的缓冲区和缓冲区和物理内存之间的锁的所有权，并从 SAN 服务提供商的缓存和从 SAN NIC 缓冲区注册删除缓冲区

<a href="" id="wsprdmaread"></a>[**WSPRdmaRead**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566304(v=vs.85))  
将数据从套接字的远程对等方可以访问的地址空间中的 RDMA 缓冲区传输到本地套接字可以访问的地址空间中的缓冲区。

<a href="" id="wsprdmawrite"></a>[**WSPRdmaWrite**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566306(v=vs.85))  
将数据从本地套接字可以访问的地址空间中的源缓冲区传输到目标的 RDMA 缓冲区中的套接字的远程对等方可以访问的地址空间。

 

 





