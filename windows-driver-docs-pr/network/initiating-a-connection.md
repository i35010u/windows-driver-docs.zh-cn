---
title: 启动的连接
description: 启动的连接
ms.assetid: 5e5ab033-b01a-45e2-acd4-7ea8931a621d
keywords:
- SAN 连接安装 WDK，启动连接
- 启动 SAN 连接
- 销毁 SAN 套接字 WDK San
- 会话协商 WDK San
- SAN 连接安装 WDK，数据流关系图
- SAN 套接字 WDK，启动连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff266f71080f3b8cee150d6344405dffde130562
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527035"
---
# <a name="initiating-a-connection"></a>启动的连接


Windows 套接字后交换机接收**WSPConnect**由应用程序，此开关启动的调用进行比较的连接请求的目标地址的 IP 子网的交换机的表中的地址与该 SAN 服务提供程序提供服务。 如果任一这些子网中包括此目标地址，调用该交换机[ **WSPSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566319)并[ **WSPBind** ](https://msdn.microsoft.com/library/windows/hardware/ff566268)的函数相应的 SAN 服务提供商联系以创建和绑定套接字时，如中所述[创建和绑定 SAN 套接字](creating-and-binding-san-sockets.md)。 应用程序的连接的交换机进程请求使用 SAN 套接字。 如果连接请求的目标地址不是 SAN 子网或 SAN 服务提供程序无法创建和绑定套接字，该开关使用 TCP/IP 提供程序建立连接。

下图显示的 Windows 套接字如何切换请求概述与远程对等方的连接。 序列和后续部分描述了更多详细信息中的连接请求。

![请求与远程对等连接时的 windows 套接字如何切换关系图概述](images/apiflow3.png)

创建并绑定 SAN 套接字之后, 该交换机执行连接请求，使用中的 SAN 套接字*非阻止模式下*，如以下过程中所述。

**若要执行连接请求**

1.  此开关调用 SAN 服务提供商[ **WSPEventSelect** ](https://msdn.microsoft.com/library/windows/hardware/ff566287)函数。 在此调用，此开关传递 FD\_CONNECT 代码和要与该代码相关联的事件对象。 在调用**WSPEventSelect**请求连接事件的通知，并通知 SAN 服务提供商的任何后续[ **WSPConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff566275)调用中执行阻止模式。

2.  之后**WSPEventSelect**函数返回时，此开关调用 SAN 服务提供商**WSPConnect**函数。 在此调用中，此开关将目标地址传递之一的格式[WSK 地址系列](https://msdn.microsoft.com/library/windows/hardware/ff571151)。 SAN 服务提供商的代理驱动程序将此目标地址映射到本机通讯，并尝试建立连接。

3.  如果 SAN 服务提供商**WSPConnect**函数可以完成或立即失败连接操作，则返回相应的成功或失败代码。 如果 SAN 服务提供商**WSPConnect**函数不能立即完成连接请求，将继续在另一个线程中以异步方式执行 SAN 服务提供商的连接操作。 SAN 服务提供程序的**WSPConnect**函数将返回错误消息 WSAEWOULDBLOCK 指示的套接字标记为非阻止性和连接操作不能立即完成的。

4.  SAN 服务提供商连接操作完成后，调用 Win32 **SetEvent**函数中以前注册的事件对象发出信号**WSPEventSelect**调用。

5.  事件对象发出信号后，此开关调用 SAN 服务提供商[ **WSPEnumNetworkEvents** ](https://msdn.microsoft.com/library/windows/hardware/ff566284)函数来获取连接操作的结果。

**请注意**  开关建立通过 SAN 服务提供商的连接后，切换不再可以为该连接使用 TCP/IP 提供程序。 SAN 服务提供商必须完全实现服务建立的连接所需的所有功能。

 

### <a name="destroying-the-san-socket"></a>销毁 SAN 套接字

如果 SAN 服务提供商**WSPConnect**函数失败，SAN 服务提供商的交换机调用[ **WSPCloseSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566273)函数来销毁 SAN 套接字。 开关然后调用 TCP/IP 服务提供商**WSPConnect**函数将转发到 TCP/IP 服务提供商连接操作，除非 SAN 服务提供程序返回以下错误代码之一的结果作为其连接操作：

<a href="" id="wsaeconnreset"></a>**WSAECONNRESET**  
指示没有任何应用程序正在侦听指定端口的目标地址

<a href="" id="wsaeconnrefused"></a>**WSAECONNREFUSED**  
指示远程应用程序主动拒绝连接请求

<a href="" id="wsaehostunreach"></a>**WSAEHOSTUNREACH**  
指示目标地址不存在

这些前面的错误代码保证在尝试建立通过 TCP/IP 连接也将失败。 如果它不能确保这一点，SAN 服务提供程序必须返回这些错误代码之一。 例如，如果目标计算机不支持 Windows 套接字直接在 SAN 上存在，但可以仅通过 NDIS 进行通信，SAN 服务提供程序不能返回 WSAEHOSTUNREACH 作为失败的 SAN 连接请求的结果到此目标中，因为通过 TCP/IP 访问接口的连接请求可能会成功。 在这种情况下，SAN 服务提供程序应返回 WSAETIMEDOUT。

### <a name="session-negotiation"></a>会话协商

切换开关建立通过 SAN 服务提供商的连接后，调用 SAN 服务提供商[ **WSPRegisterMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566311)扩展函数以预先注册的缓冲区的内存要接收传入消息的数组。 开关接下来，调用 SAN 服务提供商[ **WSPRecv** ](https://msdn.microsoft.com/library/windows/hardware/ff566309)函数发布一个或多个缓冲区，以接收来自远程对等方的传入消息的数据。 开关然后通过交换包含初始流控制信息的消息的一对协商与其远程对等方的会话。 此开关的协商会话后，它完成**WSPConnect**调用的应用程序启动。 然后，应用程序可以开始在连接上的发送和接收数据。 有关详细信息，请参阅[接受连接请求](accepting-connection-requests.md)。

通过 SAN 套接字建立连接后，此开关不会调用 SAN 服务提供商**WSPConnect**函数。 开关在内部处理的应用程序向交换机的发起呼叫**WSPConnect**函数来轮询连接请求。

 

 





