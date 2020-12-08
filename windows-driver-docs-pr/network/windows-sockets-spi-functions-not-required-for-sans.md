---
title: SAN 不需要的 Windows Sockets SPI 函数
description: SAN 不需要的 Windows Sockets SPI 函数
keywords:
- SAN 服务提供程序 WDK，不需要的功能
- 函数 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 464b1a05ffe599b89b9c197854eced10b2536d02
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821859"
---
# <a name="windows-sockets-spi-functions-not-required-for-sans"></a>SAN 不需要的 Windows Sockets SPI 函数





本部分介绍不需要 SAN 服务提供商实现的 Windows 套接字 SPI 功能。 这些函数在 Ws2spi 中定义。

<a href="" id="wspaddresstostring"></a>**WSPAddressToString**  
Windows 套接字交换机使用 TCP/IP 提供程序将 SOCKADDR 结构的所有组件转换为可读的数字字符串，该字符串表示套接字的 IP 地址。

<a href="" id="wspasyncselect"></a>**WSPAsyncSelect**  
如有必要，Windows 套接字交换机会在内部使用其会话协议来处理套接字的网络事件的通知。

<a href="" id="wspcancelblockingcall"></a>**WSPCancelBlockingCall**  
Windows 套接字交换机在内部处理正在进行的阻止请求的取消。 因此，它不会对 SAN 服务提供程序 DLL 发出取消阻止调用。 Windows 套接字交换机可以：

关闭 SAN 套接字，取消未完成的连接请求。 SAN 服务提供程序 DLL 应中止连接请求。

如果交换机在内部缓冲数据，或等待这些请求完成（如果它们是 RDMA 向应用程序缓冲区传输）或从应用程序缓冲区传输，则取消未完成的发送和接收请求。 对于较长的 RDMA 传输，开关可以完全关闭连接。

Microsoft Windows SDK 中的 Windows 套接字 SPI 文档警告，如果取消阻止调用，则应用程序不能依赖于保留的连接。 在这种情况下，在取消阻塞请求之后，保证在套接字上成功的唯一调用是 **WSPCloseSocket**。

**WSPGetPeerName** 当交换机在 **WSPConnect** 调用中建立与对等方的连接，或者在 **WSPAccept** 调用中接受到对等方的连接时，Windows 套接字交换机会缓存该对等节点的 IP 地址。 如果需要，此开关将为应用程序提供此缓存值。

**WSPGetSockName** 当交换机在 **WSPBind** 调用中将地址与套接字关联时，Windows 套接字交换机会缓存套接字的本地 IP 地址，或接受 **WSPAccept** 调用中与对等方的连接。 如果需要，此开关将为应用程序提供此缓存值。

**WSPJoinLeaf** Windows 套接交换机独占使用 TCP/IP 提供程序来处理 multipoint 会话。

**WSPRecvDisconnect** Windows 套接字交换机在内部处理套接字上数据接收的终止，并从远程方检索任何传入的断开连接数据。

**WSPRecvFrom** Windows 套接字直通的当前版本不支持 SAN 服务提供程序处理套接字，该套接字通过用户数据报协议 (UDP) 语义接收数据报。 因此，Windows 套接交换机会在连接的套接字上调用 SAN 服务提供程序的 **WSPRecv** 函数，以使用传输控制协议 (TCP) 语义接收流数据。

**WSPSelect** Windows 套接字交换机在内部与 TCP/IP 提供程序协作使用其会话协议，以根据需要确定套接字的状态。

**WSPSendDisconnect** Windows 套接字交换机在内部处理套接字的连接终止，并向远程方发送断开连接的数据。

**WSPSendTo** Windows 套接字直通的当前版本不支持 SAN 服务提供程序处理套接字，该套接字通过用户数据报协议 (UDP) 语义发送数据报。 因此，Windows 套接交换机会在连接的套接字上调用 SAN 服务提供程序的 **WSPSend** 函数，以使用传输控制协议 (TCP) 语义发送流数据。

**WSPShutdown** Windows 套接字交换机在内部禁用套接字上数据的接收和传输。

**WSPStartup** Windows 套接交换机不会调用 **WSPStartup** 来启动 SAN 服务提供程序的操作。 交换机改用 SAN 服务提供商的 **WSPStatupEx** 函数。

**WSPStringToAddress** Windows 套接字交换机使用 TCP/IP 提供程序将代表套接字 IP 地址的用户可读数字字符串转换为 (SOCKADDR) 的套接字地址结构，该结构适合传递到采用此类结构的 Windows 套接字例程。

 

 





