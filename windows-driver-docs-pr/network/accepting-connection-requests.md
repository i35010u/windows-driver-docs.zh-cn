---
title: 接受连接请求
description: 接受连接请求
ms.assetid: 2233daa7-c5c5-49be-b76e-61a90a496447
keywords:
- SAN 连接安装 WDK，接受连接请求
- 传入的连接请求 WDK San
- 会话协商 WDK San
- 远程对等方连接请求 WDK San
- 接受连接请求 WDK San
- 拒绝 SAN 连接请求
- 拒绝 SAN 连接请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5af6ebea57f29ca06773635323cff3d9bd7719e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367835"
---
# <a name="accepting-connection-requests"></a>接受连接请求





如果应用程序调用**WSAAccept**，**接受**，或**AcceptEx**函数接受套接字上的传入连接请求，Windows 套接字始终切换将转发到 TCP/IP 服务提供程序的此调用。 如果从非 SAN 网络到达的传入连接请求，流经 NDIS 路径和 TCP/IP 服务提供商对其进行处理。 如果连接请求来自 SAN 上的远程对等方，交换机充当 TCP/IP 服务提供程序与 SAN 服务提供程序在确定是否接受连接请求和完成应用程序的之间的中介**WSAAccept**，**接受**，或**AcceptEx**函数。

下图显示的 Windows 套接字开关和 SAN 服务提供商之间的交互概述了在确定是否接受或拒绝传入的连接请求。 序列和后续部分介绍了更多详细信息中的接受决定。

![windows 套接字交换机和 san 服务提供商之间的交互的关系图概述](images/apiflow5.png)

 **若要接受或拒绝连接请求**

1.  从远程对等方收到的传入连接请求，SAN 服务提供商通知的事件对象，如中所述[侦听连接在 SAN 上](listening-for-connections-on-a-san.md)。

2.  Windows 套接字切换调用 SAN 服务提供商[ **WSPEnumNetworkEvents** ](https://msdn.microsoft.com/library/windows/hardware/ff566284)函数来接收 FD\_接受事件代码。

3.  在接收 FD\_接受事件的代码中，此开关调用 SAN 服务提供商[ **WSPAccept** ](https://msdn.microsoft.com/library/windows/hardware/ff566266)函数接受或拒绝传入的连接请求。

4.  对 SAN 服务提供商的交换机的调用中[ **WSPAccept** ](https://msdn.microsoft.com/library/windows/hardware/ff566266)函数，该开关指定的条件函数。 SAN 服务提供程序必须将此条件函数所在的同一线程中调用**WSPAccept**从返回前调用函数**WSPAccept**调用。

5.  Switch 返回 CF\_接受或 CF\_拒绝代码从该条件函数，以指示它接受或拒绝连接请求，分别。

### <a name="accepting-a-connection-request-and-creating-an-accepting-socket"></a>接受连接请求并创建接受的套接字

如果应用程序接受传入连接请求，则 switch 返回 CF\_SAN 服务提供程序以完成将开关的条件函数接受代码。 在接收到 CF\_接受，SAN 服务提供程序初始化内部数据结构，它将在其中存储有关接受的套接字信息。 SAN 服务提供商[ **WSPAccept** ](https://msdn.microsoft.com/library/windows/hardware/ff566266)函数接下来必须调用**WPUCreateSocketHandle**函数获取交换机中接受的套接字的描述符. SAN 服务提供商必须存储在其内部数据结构，用于接受的套接字的交换机的描述符，并且必须返回接受的套接字以完成自己描述符**WSPAccept**调用。 交换机必须提供 SAN 服务提供商的内部描述符接受的套接字时调用 SAN 服务提供程序的函数，而 SAN 服务提供商必须提供中对此开关的交换机的套接字描述符。

已成功完成之前[ **WSPAccept**](https://msdn.microsoft.com/library/windows/hardware/ff566266)，SAN 服务提供程序应调用 Win32 **ResetEvent**函数以重置事件对象。 执行可以让 SAN 服务提供商，以更高版本调用 Win32 **SetEvent**函数以指示该开关可接受的下一步的传入连接请求。

### <a name="rejecting-a-connection-request"></a>拒绝连接请求

如果应用程序将拒绝传入的连接请求，则 switch 返回 CF\_拒绝到 SAN 服务提供程序来完成开关的条件函数的代码。 在接收到 CF\_拒绝，SAN 服务提供程序应返回 WSAECONNREFUSED 错误代码，到完成的交换机[ **WSPAccept** ](https://msdn.microsoft.com/library/windows/hardware/ff566266)调用。

### <a name="indicating-acceptance-or-refusal-of-a-connection-request-to-a-remote-peer"></a>指示接受或拒绝连接请求发送到远程对等方的消息

SAN 服务提供商可以向远程对等方指示，它接受或拒绝远程对等节点的连接请求之前，SAN 服务提供程序必须调用开关的条件函数。 具体取决于交换机的条件函数返回的值，SAN 服务提供商应使以下迹象之一向远程对等方：

如果将开关的条件函数返回 CF\_接受，SAN 服务提供商应指示它接受远程对等节点的连接请求。 然后，远程对等方上的 SAN 服务提供程序才能成功完成时启动了其连接操作[ **WSPConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff566275)调用。

如果将开关的条件函数返回 CF\_拒绝，SAN 服务提供商应指示，它将拒绝远程对等节点的连接请求。 远程对等方上的 SAN 服务提供程序必须由启动其连接操作失败[ **WSPConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff566275) WSAECONNREFUSED 错误代码调用。

### <a name="session-negotiation"></a>会话协商

已成功使用开关 SAN 服务提供程序接受来自远程对等方的连接请求后，该交换机协商与该对等方的会话。

 **若要协商会话**

1.  在远程对等方 switch 调用 SAN 服务提供商[ **WSPRecv** ](https://msdn.microsoft.com/library/windows/hardware/ff566309)发布的一组接收缓冲区的函数。

2.  在远程对等方 switch 调用 SAN 服务提供商[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)函数将会话协商消息发送到在本地接受终结点上的交换机。 此消息包含在远程对等方 switch 发布的接收缓冲区的数目。

3.  在本地接受终结点上的交换机调用本地 SAN 服务提供商[ **WSPRecv** ](https://msdn.microsoft.com/library/windows/hardware/ff566309)发布其自己的函数接收缓冲区，但它可能不能为此，要接收该会话的时间协商消息。 如果本地开关在时间中未发布接收缓冲区和 SAN 基础 NIC 不支持流控制，如果服务提供商在本地接受终结点必须在其自己专用的接收缓冲区中缓冲远程交换机的会话协商消息。 当交换机文章接收缓冲区时，SAN 服务提供商将数据复制从其专用的接收缓冲区到在一对一基础上的交换机缓冲区之前的所有数据已从复制专用缓冲区开关的缓冲区。

    SAN 服务提供程序执行正常接收处理后续交换机缓冲区-即，在 NIC 上发到接收队列所有此类交换机缓冲区

    请注意，SAN 服务提供商必须只需删除连接因为会话协商消息到达之前，此开关不未发布接收缓冲区。 会话协商消息的最大长度为 256 个字节。

4.  在本地接受终结点上的交换机对应于会话协商消息之前发送其接收缓冲区。 本地切换调用本地 SAN 服务提供商[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)函数对会话协商消息做出响应。 将本地开关的响应包括本地开关发布的接收缓冲区的数目。 从这一刻起，本地开关可保证已发布的一组接收缓冲区足够大的可接收到达连接上的任何消息。

5.  如果应用程序为指定的初始接收缓冲区中其**AcceptEx**调用，将该交换机等待，直到完成该应用程序之前从其远程对等方收到第一个数据消息**AcceptEx**调用。

6.  如果应用程序将取消其自身**接受**调用时，此开关调用相应 SAN 服务提供商[ **WSPCloseSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566273)函数以关闭接受的 SAN 套接字.

 

 





