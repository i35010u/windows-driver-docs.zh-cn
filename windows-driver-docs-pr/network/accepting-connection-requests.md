---
title: 接受连接请求
description: 接受连接请求
keywords:
- SAN 连接设置 WDK，接受连接请求
- 传入连接请求 WDK San
- 会话协商 WDK San
- 远程对等连接请求 WDK San
- 接受连接请求 WDK San
- 拒绝 SAN 连接请求
- 拒绝 SAN 连接请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e99f93ce11411b48a86762fabf50c7aad2775a51
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836797"
---
# <a name="accepting-connection-requests"></a>接受连接请求





如果应用程序调用 **WSAAccept**、 **accept** 或 **AcceptEx** 函数来接受套接字上的传入连接请求，则 Windows 套接交换机始终会将此调用转发到 tcp/ip 服务提供商。 如果传入连接请求到达非 SAN 网络，则会流过 NDIS 路径，并且 TCP/IP 服务提供程序将处理该请求。 如果连接请求到达 SAN 上的远程对等方，则该开关将充当 TCP/IP 服务提供程序与 SAN 服务提供商之间的中介，以确定是否接受连接请求以及在完成应用程序的 **WSAAccept**、 **accept** 或 **AcceptEx** 函数。

下图显示了用于确定是接受还是拒绝传入连接请求的 Windows 套接字交换机与 SAN 服务提供商之间的交互的概述。 下面的序列和部分更详细地介绍了接受决定。

![windows 套接字交换机与 san 服务提供商之间的交互的关系图概述](images/apiflow5.png)

 **接受或拒绝连接请求**

1.  收到来自远程对等方的传入连接请求时，SAN 服务提供程序会根据在 [SAN 上侦听连接](listening-for-connections-on-a-san.md)中所述发出事件对象的信号。

2.  Windows 套接交换机调用 SAN 服务提供商的 [**WSPEnumNetworkEvents**](/previous-versions/windows/hardware/network/ff566284(v=vs.85)) 函数来接收 FD \_ ACCEPT 事件代码。

3.  接收到 FD \_ ACCEPT 事件代码时，开关会调用 SAN 服务提供程序的 [**WSPAccept**](/previous-versions/windows/hardware/network/ff566266(v=vs.85)) 函数，以接受或拒绝传入连接请求。

4.  在开关对 SAN 服务提供程序的 [**WSPAccept**](/previous-versions/windows/hardware/network/ff566266(v=vs.85)) 函数的调用中，开关指定条件函数。 在从 **WSPAccept** 调用返回之前，SAN 服务提供程序必须在调用 **WSPAccept** 函数的同一线程中调用此条件函数。

5.  开关将 \_ 从该条件函数返回 CF ACCEPT 或 cf \_ 拒绝代码，以指示它分别接受或拒绝连接请求。

### <a name="accepting-a-connection-request-and-creating-an-accepting-socket"></a>接受连接请求并创建接受套接字

如果应用程序接受传入的连接请求，则交换机会将 CF \_ ACCEPT 代码返回到 SAN 服务提供商，以完成交换机的 condition 函数。 接收 CF \_ ACCEPT 后，SAN 服务提供程序将初始化内部数据结构，在该结构中存储有关接受套接字的信息。 SAN 服务提供程序的 [**WSPAccept**](/previous-versions/windows/hardware/network/ff566266(v=vs.85)) 函数必须接下来调用 **WPUCreateSocketHandle** 函数，以从交换机获取接受套接字的描述符。 SAN 服务提供程序必须将交换机的描述符存储在接受套接字的内部数据结构中，并且必须为接受套接字返回其自己的描述符才能完成 **WSPAccept** 调用。 调用 SAN 服务提供程序的函数时，此开关必须为接受套接字提供 SAN 服务提供程序的内部描述符，而 SAN 服务提供程序必须在对交换机的调用中提供交换机的套接字描述符。

在成功完成 [**WSPAccept**](/previous-versions/windows/hardware/network/ff566266(v=vs.85))之前，SAN 服务提供程序应调用 Win32 **ResetEvent** 函数来重置事件对象。 这样一来，SAN 服务提供商稍后就可以调用 Win32 **SetEvent** 函数，以指示开关接受下一个传入连接请求。

### <a name="rejecting-a-connection-request"></a>拒绝连接请求

如果应用程序拒绝传入连接请求，则交换机会将 CF \_ 拒绝代码返回到 SAN 服务提供商，以完成交换机的 condition 函数。 收到 CF \_ 拒绝后，SAN 服务提供商应将 WSAECONNREFUSED 错误代码返回到开关以完成 [**WSPAccept**](/previous-versions/windows/hardware/network/ff566266(v=vs.85)) 调用。

### <a name="indicating-acceptance-or-refusal-of-a-connection-request-to-a-remote-peer"></a>指示接受或拒绝到远程对等方的连接请求

在 SAN 服务提供商可以向远程对等机指示它接受或拒绝远程对等方的连接请求之前，SAN 服务提供程序必须调用交换机的 condition 函数。 根据交换机的 condition 函数返回的值，SAN 服务提供商应向远程对等机发出以下指示之一：

如果开关的 condition 函数返回 CF \_ ACCEPT，则 SAN 服务提供程序应指示它接受远程对等方的连接请求。 远程对等方上的 SAN 服务提供商可以成功完成由 [**WSPConnect**](/previous-versions/windows/hardware/network/ff566275(v=vs.85)) 调用启动的连接操作。

如果开关的 condition 函数返回 CF \_ 拒绝，则 SAN 服务提供程序应指示它拒绝远程对等方的连接请求。 远程对等方上的 SAN 服务提供程序必须使用 WSAECONNREFUSED 错误代码将 [**WSPConnect**](/previous-versions/windows/hardware/network/ff566275(v=vs.85)) 调用启动的连接操作失败。

### <a name="session-negotiation"></a>会话协商

在交换机成功使用 SAN 服务提供商接受来自远程对等方的连接请求后，该交换机会与该对等节点协商会话。

 **协商会话**

1.  远程对等机上的开关调用 SAN 服务提供程序的 [**WSPRecv**](/previous-versions/windows/hardware/network/ff566309(v=vs.85)) 函数，以发布一组接收缓冲区。

2.  远程对等机上的开关调用 SAN 服务提供程序的 [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85)) 函数，以将会话协商消息发送到本地接受终结点上的开关。 此消息包括远程对等节点上发送的交换机的接收缓冲区数。

3.  位于本地接受终结点的开关调用本地 SAN 服务提供程序的 [**WSPRecv**](/previous-versions/windows/hardware/network/ff566309(v=vs.85)) 函数来发布其自己的接收缓冲区，但它可能无法及时接收会话协商消息。 如果本地交换机不会按时发布接收缓冲区，并且基础 NIC 不支持流控制，则位于本地接受终结点上的 SAN 服务提供程序必须在其自己的专用接收缓冲区中缓冲远程交换机的会话协商消息。 当交换机发布接收缓冲区时，SAN 服务提供程序将数据从其专用接收缓冲区复制到交换机缓冲区，直到将所有数据从专用缓冲区复制到切换缓冲区。

    SAN 服务提供程序在后续切换缓冲区上执行常规接收处理，即，它将所有此类切换缓冲区发送到 NIC 上的接收队列。

    请注意，SAN 服务提供商不能直接删除连接，因为在会话协商消息到达之前，交换机不会发布接收缓冲区。 会话协商消息的最大长度为256个字节。

4.  位于本地接受终结点的开关将在响应会话协商消息之前发布其接收缓冲区。 本地交换机调用本地 SAN 服务提供商的 [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85)) 函数来响应会话协商消息。 本地交换机的响应包括本地交换机投递的接收缓冲区数。 从这个角度来，本地交换机可保证发送的接收缓冲区的大小足以接收到连接上的任何消息。

5.  如果应用程序在其 **AcceptEx** 调用中指定了初始接收缓冲区，则该开关将等待，直到它在完成应用程序的 **AcceptEx** 调用之前从其远程对等方收到第一个数据消息。

6.  如果应用程序取消自己的 **accept** 调用，则交换机将调用相应的 san 服务提供程序的 [**WSPCloseSocket**](/previous-versions/windows/hardware/network/ff566273(v=vs.85)) 函数来关闭接受的 san 套接字。

 

