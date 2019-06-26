---
title: SAN 所需的 Windows Sockets SPI 函数
description: SAN 所需的 Windows Sockets SPI 函数
ms.assetid: b41bd7e0-bb6c-4933-a5d0-18e4d067601b
keywords:
- SAN 服务提供商 WDK，所需的功能
- WDK San 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b0cc60baa81b749ac1bf977adbb81f83d658d5e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384698"
---
# <a name="windows-sockets-spi-functions-required-for-sans"></a>SAN 所需的 Windows Sockets SPI 函数





本部分介绍 Windows 套接字 SPI SAN 服务提供程序 DLL 必须提供的函数。 这些函数在 Ws2spi.h 中定义并完全记录在[Windows 套接字直接引用](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565857(v=vs.85))部分：

<a href="" id="wspaccept"></a>[**WSPAccept**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566266(v=vs.85))  
有条件地接受套接字侦听基于提供的条件函数的返回值的连接的连接。

<a href="" id="wspbind"></a>[**WSPBind**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566268(v=vs.85))  
将相关联的本地 IP 地址或使用套接字网络接口的名称。 此网络接口是由 SAN 服务提供商提供服务。

<a href="" id="wspcleanup"></a>[**WSPCleanup**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566270(v=vs.85))  
终止使用 SAN 服务提供程序 DLL。

<a href="" id="wspclosesocket"></a>[**WSPCloseSocket**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566273(v=vs.85))  
关闭套接字。

<a href="" id="wspconnect"></a>[**WSPConnect**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566275(v=vs.85))  
建立连接的对等方套接字时，交换连接数据，并指定所需的服务质量 (QoS) 基于提供的流规范。

<a href="" id="wspduplicatesocket"></a>[**WSPDuplicateSocket**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566282(v=vs.85))  
检索 WSAPROTOCOL\_INFOW 结构，它可用于在另一个进程的上下文中创建新共享的套接字的套接字描述符。

<a href="" id="wspenumnetworkevents"></a>[**WSPEnumNetworkEvents**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566284(v=vs.85))  
将报告为套接字的网络事件的出现次数。

<a href="" id="wspeventselect"></a>[**WSPEventSelect**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566287(v=vs.85))  
指定套接字的事件对象。 此事件对象随后将由提供的一组网络事件的匹配项。

<a href="" id="wspgetoverlappedresult"></a>[**WSPGetOverlappedResult**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566288(v=vs.85))  
返回套接字上异步 （重叠） 操作的结果。 此操作以前指示它正在等待完成。

<a href="" id="wspgetqosbyname"></a>[**WSPGetQOSByName**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566290(v=vs.85))  
初始化基于命名模板，QoS 结构或检索可用的模板名称的枚举。

必须完全实现 SAN 服务提供程序 DLL，支持 QoS **WSPGetQOSByName**。 如果 SAN 服务提供了不支持 QoS，其**WSPGetQOSByName**函数必须至少返回错误 WSAEOPNOTSUPP。

<a href="" id="wspgetsockopt"></a>[**WSPGetSockOpt**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566292(v=vs.85))  
检索一个套接字选项的当前值。

<a href="" id="wspioctl"></a>[**WSPIoctl**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566296(v=vs.85))  
设置或检索与套接字关联的操作参数。

<a href="" id="wsplisten"></a>[**WSPListen**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566297(v=vs.85))  
建立套接字来侦听传入连接。

<a href="" id="wsprecv"></a>[**WSPRecv**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566309(v=vs.85))  
接收连接的套接字上的数据。

<a href="" id="wspsend"></a>[**WSPSend**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566316(v=vs.85))  
在连接的套接字上发送数据。

<a href="" id="wspsetsockopt"></a>[**WSPSetSockOpt**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566318(v=vs.85))  
设置套接字选项的值。

<a href="" id="wspsocket"></a>[**WSPSocket**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566319(v=vs.85))  
创建使用 TCP/IP 协议和异步 （重叠） 的数据传输的套接字。

 

 





