---
title: SAN 所需的 Windows Sockets SPI 函数
description: SAN 所需的 Windows Sockets SPI 函数
ms.assetid: b41bd7e0-bb6c-4933-a5d0-18e4d067601b
keywords:
- SAN 服务提供商 WDK，所需的功能
- WDK San 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9da03118f624130a3465120f7f6b8be82139315
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382857"
---
# <a name="windows-sockets-spi-functions-required-for-sans"></a>SAN 所需的 Windows Sockets SPI 函数





本部分介绍 Windows 套接字 SPI SAN 服务提供程序 DLL 必须提供的函数。 这些函数在 Ws2spi.h 中定义并完全记录在[Windows 套接字直接引用](https://msdn.microsoft.com/library/windows/hardware/ff565857)部分：

<a href="" id="wspaccept"></a>[**WSPAccept**](https://msdn.microsoft.com/library/windows/hardware/ff566266)  
有条件地接受套接字侦听基于提供的条件函数的返回值的连接的连接。

<a href="" id="wspbind"></a>[**WSPBind**](https://msdn.microsoft.com/library/windows/hardware/ff566268)  
将相关联的本地 IP 地址或使用套接字网络接口的名称。 此网络接口是由 SAN 服务提供商提供服务。

<a href="" id="wspcleanup"></a>[**WSPCleanup**](https://msdn.microsoft.com/library/windows/hardware/ff566270)  
终止使用 SAN 服务提供程序 DLL。

<a href="" id="wspclosesocket"></a>[**WSPCloseSocket**](https://msdn.microsoft.com/library/windows/hardware/ff566273)  
关闭套接字。

<a href="" id="wspconnect"></a>[**WSPConnect**](https://msdn.microsoft.com/library/windows/hardware/ff566275)  
建立连接的对等方套接字时，交换连接数据，并指定所需的服务质量 (QoS) 基于提供的流规范。

<a href="" id="wspduplicatesocket"></a>[**WSPDuplicateSocket**](https://msdn.microsoft.com/library/windows/hardware/ff566282)  
检索 WSAPROTOCOL\_INFOW 结构，它可用于在另一个进程的上下文中创建新共享的套接字的套接字描述符。

<a href="" id="wspenumnetworkevents"></a>[**WSPEnumNetworkEvents**](https://msdn.microsoft.com/library/windows/hardware/ff566284)  
将报告为套接字的网络事件的出现次数。

<a href="" id="wspeventselect"></a>[**WSPEventSelect**](https://msdn.microsoft.com/library/windows/hardware/ff566287)  
指定套接字的事件对象。 此事件对象随后将由提供的一组网络事件的匹配项。

<a href="" id="wspgetoverlappedresult"></a>[**WSPGetOverlappedResult**](https://msdn.microsoft.com/library/windows/hardware/ff566288)  
返回套接字上异步 （重叠） 操作的结果。 此操作以前指示它正在等待完成。

<a href="" id="wspgetqosbyname"></a>[**WSPGetQOSByName**](https://msdn.microsoft.com/library/windows/hardware/ff566290)  
初始化基于命名模板，QoS 结构或检索可用的模板名称的枚举。

必须完全实现 SAN 服务提供程序 DLL，支持 QoS **WSPGetQOSByName**。 如果 SAN 服务提供了不支持 QoS，其**WSPGetQOSByName**函数必须至少返回错误 WSAEOPNOTSUPP。

<a href="" id="wspgetsockopt"></a>[**WSPGetSockOpt**](https://msdn.microsoft.com/library/windows/hardware/ff566292)  
检索一个套接字选项的当前值。

<a href="" id="wspioctl"></a>[**WSPIoctl**](https://msdn.microsoft.com/library/windows/hardware/ff566296)  
设置或检索与套接字关联的操作参数。

<a href="" id="wsplisten"></a>[**WSPListen**](https://msdn.microsoft.com/library/windows/hardware/ff566297)  
建立套接字来侦听传入连接。

<a href="" id="wsprecv"></a>[**WSPRecv**](https://msdn.microsoft.com/library/windows/hardware/ff566309)  
接收连接的套接字上的数据。

<a href="" id="wspsend"></a>[**WSPSend**](https://msdn.microsoft.com/library/windows/hardware/ff566316)  
在连接的套接字上发送数据。

<a href="" id="wspsetsockopt"></a>[**WSPSetSockOpt**](https://msdn.microsoft.com/library/windows/hardware/ff566318)  
设置套接字选项的值。

<a href="" id="wspsocket"></a>[**WSPSocket**](https://msdn.microsoft.com/library/windows/hardware/ff566319)  
创建使用 TCP/IP 协议和异步 （重叠） 的数据传输的套接字。

 

 





