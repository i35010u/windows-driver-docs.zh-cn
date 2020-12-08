---
title: SAN 所需的 Windows Sockets SPI 函数
description: SAN 所需的 Windows Sockets SPI 函数
keywords:
- SAN 服务提供商 WDK，必需的功能
- 函数 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f5b75dacbce6461305b6610e2c3e55a98e039c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834029"
---
# <a name="windows-sockets-spi-functions-required-for-sans"></a>SAN 所需的 Windows Sockets SPI 函数





本部分介绍了 SAN 服务提供程序 DLL 必须提供的 Windows 套接字 SPI 功能。 这些函数在 Ws2spi 中定义，并在 [Windows 套接字直接参考](/previous-versions/windows/hardware/network/ff565857(v=vs.85)) 部分中完整记录：

<a href="" id="wspaccept"></a>[**WSPAccept**](/previous-versions/windows/hardware/network/ff566266(v=vs.85))  
根据提供的条件函数的返回值，有条件地接受侦听连接的套接字的连接。

<a href="" id="wspbind"></a>[**WSPBind**](/previous-versions/windows/hardware/network/ff566268(v=vs.85))  
将网络接口的本地 IP 地址（或名称）与套接字关联。 此网络接口由 SAN 服务提供商提供服务。

<a href="" id="wspcleanup"></a>[**WSPCleanup**](/previous-versions/windows/hardware/network/ff566270(v=vs.85))  
终止使用 SAN 服务提供程序 DLL。

<a href="" id="wspclosesocket"></a>[**WSPCloseSocket**](/previous-versions/windows/hardware/network/ff566273(v=vs.85))  
关闭套接字。

<a href="" id="wspconnect"></a>[**WSPConnect**](/previous-versions/windows/hardware/network/ff566275(v=vs.85))  
建立套接字到对等方的连接，交换连接数据，并根据提供的流规范指定 (QoS) 所需的服务质量。

<a href="" id="wspduplicatesocket"></a>[**WSPDuplicateSocket**](/previous-versions/windows/hardware/network/ff566282(v=vs.85))  
检索 \_ 可用于在另一个进程的上下文中为共享套接字创建新套接字描述符的 WSAPROTOCOL INFOW 结构。

<a href="" id="wspenumnetworkevents"></a>[**WSPEnumNetworkEvents**](/previous-versions/windows/hardware/network/ff566284(v=vs.85))  
报告套接字的网络事件发生。

<a href="" id="wspeventselect"></a>[**WSPEventSelect**](/previous-versions/windows/hardware/network/ff566287(v=vs.85))  
指定套接字的事件对象。 此事件对象随后由提供的一组网络事件设置。

<a href="" id="wspgetoverlappedresult"></a>[**WSPGetOverlappedResult**](/previous-versions/windows/hardware/network/ff566288(v=vs.85))  
返回对套接字的异步 (重叠) 操作的结果。 此操作之前指示它正在等待完成。

<a href="" id="wspgetqosbyname"></a>[**WSPGetQOSByName**](/previous-versions/windows/hardware/network/ff566290(v=vs.85))  
基于命名模板初始化 QoS 结构，或检索可用模板名称的枚举。

支持 QoS 的 SAN 服务提供程序 DLL 必须完全实现 **WSPGetQOSByName**。 如果 SAN 服务提供不支持 QoS，则其 **WSPGetQOSByName** 函数必须至少返回错误 WSAEOPNOTSUPP。

<a href="" id="wspgetsockopt"></a>[**WSPGetSockOpt**](/previous-versions/windows/hardware/network/ff566292(v=vs.85))  
检索套接字的选项的当前值。

<a href="" id="wspioctl"></a>[**WSPIoctl**](/previous-versions/windows/hardware/network/ff566296(v=vs.85))  
设置或检索与套接字关联的操作参数。

<a href="" id="wsplisten"></a>[**WSPListen**](/previous-versions/windows/hardware/network/ff566297(v=vs.85))  
建立用于侦听传入连接的套接字。

<a href="" id="wsprecv"></a>[**WSPRecv**](/previous-versions/windows/hardware/network/ff566309(v=vs.85))  
接收连接的套接字上的数据。

<a href="" id="wspsend"></a>[**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85))  
在连接的套接字上发送数据。

<a href="" id="wspsetsockopt"></a>[**WSPSetSockOpt**](/previous-versions/windows/hardware/network/ff566318(v=vs.85))  
为套接字设置选项的值。

<a href="" id="wspsocket"></a>[**WSPSocket**](/previous-versions/windows/hardware/network/ff566319(v=vs.85))  
使用 TCP/IP 协议和异步 (重叠) 数据传输创建套接字。

 

