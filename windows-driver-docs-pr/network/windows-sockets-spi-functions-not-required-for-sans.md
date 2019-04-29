---
title: SAN 不需要的 Windows Sockets SPI 函数
description: SAN 不需要的 Windows Sockets SPI 函数
ms.assetid: 995ff59e-8ee4-4468-914d-47c14d804c38
keywords:
- SAN 服务提供商 WDK，不是必需的函数
- WDK San 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81b8690c37dda4cdb43b38827073aeae97a46421
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365679"
---
# <a name="windows-sockets-spi-functions-not-required-for-sans"></a>SAN 不需要的 Windows Sockets SPI 函数





本部分介绍 Windows 套接字 SPI SAN 服务提供程序不需要实现的函数。 这些函数 Ws2spi.h 中定义。

<a href="" id="wspaddresstostring"></a>**WSPAddressToString**  
Windows 套接字开关使用 TCP/IP 提供程序的 SOCKADDR 结构的所有组件都转换为人工可读的数字字符串表示套接字的 IP 地址。

<a href="" id="wspasyncselect"></a>**WSPAsyncSelect**  
Windows 套接字交换机其会话协议在内部使用以处理通知的网络事件的套接字时，如有必要。

<a href="" id="wspcancelblockingcall"></a>**WSPCancelBlockingCall**  
Windows 套接字开关在内部处理取消阻止正在进行的请求。 因此，它永远不会发出取消阻止对 SAN 服务提供程序 DLL 的调用。 Windows 套接字切换可以：

通过关闭 SAN 套接字取消未完成连接请求。 SAN 服务提供程序 DLL 应中止的连接请求。

取消未完成发送和接收请求，如果交换机缓冲该数据在内部，放弃这些请求的数据，或等待这些请求以完成它们是否 RDMA 传输到或从应用程序缓冲区。 对于耗时较长的 RDMA 传输，此开关可以完全关闭该连接。

Microsoft Windows SDK 中的 Windows 套接字 SPI 文档会发出警告，如果取消阻止调用，则应用程序将不能依赖于保留的连接。 在这种情况下，可确保成功套接字上的阻塞请求取消后的唯一调用是**WSPCloseSocket**。

**WSPGetPeerName**交换机建立在对等方的连接时，Windows 套接字开关调整缓存的对等方的 IP 地址**WSPConnect**调用，或接受与中的对等方的连接**WSPAccept**调用。 如有必要，该交换机提供对应用程序，该缓存的值。

**WSPGetSockName**开关将地址中的套接字与相关联时，Windows 套接字开关调整缓存套接字的本地 IP 地址**WSPBind**调用，或接受与中的对等连接**WSPAccept**调用。 如有必要，该交换机提供对应用程序，该缓存的值。

**WSPJoinLeaf** Windows 套接字开关以独占方式使用 TCP/IP 提供程序来处理多点会话。

**WSPRecvDisconnect** Windows 套接字开关在内部处理的数据接收套接字上终止，并检索任何传入断开与远程方的连接数据。

**WSPRecvFrom** Windows 套接字直接的当前版本不支持 SAN 服务提供商处理套接字的接收数据报与用户数据报协议 (UDP) 语义。 因此，Windows 套接字开关调用 SAN 服务提供商**WSPRecv**上连接的套接字接收和传输控制协议 (TCP) 语义的流数据的函数。

**WSPSelect** Windows 套接字切换其会话协议在内部使用与 TCP/IP 提供商合作来确定的状态套接字，如有必要。

**WSPSendDisconnect** Windows 套接字开关在内部处理套接字的连接终止，并发送断开连接到远程参与方的数据。

**WSPSendTo** Windows 套接字直接的当前版本不支持 SAN 服务提供商处理套接字的发送数据报与用户数据报协议 (UDP) 语义。 因此，Windows 套接字开关调用 SAN 服务提供商**WSPSend**上连接的套接字来发送流数据和传输控制协议 (TCP) 语义的函数。

**WSPShutdown** Windows 套接字开关从内部禁用接收和套接字上的数据的传输。

**WSPStartup** Windows 套接字开关不会调用**WSPStartup**开始 SAN 服务提供程序的操作。 交换机改为使用 SAN 服务提供商**WSPStatupEx**函数。

**WSPStringToAddress** Windows 套接字开关使用 TCP/IP 提供程序将适合将传递给 Windows 套接字的套接字地址结构 (SOCKADDR) 表示的套接字的 IP 地址的用户可读数字 string 转换采用此类结构的例程。

 

 





