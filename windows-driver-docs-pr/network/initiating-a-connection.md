---
title: 发起连接
description: 发起连接
ms.assetid: 5e5ab033-b01a-45e2-acd4-7ea8931a621d
keywords:
- SAN 连接设置 WDK，启动连接
- 启动 SAN 连接
- 销毁 SAN 套接字 WDK San
- 会话协商 WDK San
- SAN 连接设置 WDK，流程图
- SAN 套接字 WDK，启动连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55b05014001afc75ebf381411abdd287f5261998
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209313"
---
# <a name="initiating-a-connection"></a>发起连接


Windows 套接字交换机接收到由应用程序启动的 **WSPConnect** 调用后，交换机会将连接请求的目标地址与 SAN 服务提供商服务的 IP 子网交换机表中的地址进行比较。 如果其中一个子网包括此目标地址，则交换机会调用相应 SAN 服务提供商的 [**WSPSocket**](/previous-versions/windows/hardware/network/ff566319(v=vs.85)) 和 [**WSPBind**](/previous-versions/windows/hardware/network/ff566268(v=vs.85)) 函数来创建和绑定套接字，如 [创建和绑定 SAN 套接字](creating-and-binding-san-sockets.md)中所述。 交换机使用 SAN 套接字处理应用程序的连接请求。 如果连接请求的目标地址不在 SAN 子网中，或者如果 SAN 服务提供程序无法创建和绑定套接字，则交换机将使用 TCP/IP 提供程序建立连接。

下图显示了 Windows 套接交换机如何请求与远程对等机建立连接的概述。 下面的序列和部分更详细地描述了连接请求。

![图表概述 windows 套接交换机如何请求与远程对等机的连接](images/apiflow3.png)

创建并绑定 SAN 套接字后，交换机将使用处于非 *阻止模式下*的 san 套接字执行连接请求，如以下过程中所述。

**执行连接请求**

1.  开关调用 SAN 服务提供程序的 [**WSPEventSelect**](/previous-versions/windows/hardware/network/ff566287(v=vs.85)) 函数。 在此调用中，开关传递 FD \_ 连接代码和要与该代码相关联的事件对象。 对 **WSPEventSelect** 的调用请求连接事件的通知，并通知 SAN 服务提供程序在非阻止模式下执行的任何后续 [**WSPConnect**](/previous-versions/windows/hardware/network/ff566275(v=vs.85)) 调用。

2.  **WSPEventSelect**函数返回后，开关调用 SAN 服务提供程序的**WSPConnect**函数。 在此调用中，开关以 [WSK 地址系列](/previous-versions/windows/hardware/drivers/mt808757(v=vs.85))之一的格式传递目标地址。 SAN 服务提供商的代理驱动程序将此目标地址映射到本机地址，并尝试建立连接。

3.  如果 SAN 服务提供商的 **WSPConnect** 函数可以立即完成连接操作或使连接操作失败，它将返回相应的成功或失败代码。 如果 SAN 服务提供商的 **WSPConnect** 函数无法立即完成连接请求，则 san 服务提供商的连接操作会在另一个线程中以异步方式执行。 SAN 服务提供程序的 **WSPConnect** 函数返回并带有错误 WSAEWOULDBLOCK，以指示套接字标记为非阻止，并且无法立即完成连接操作。

4.  连接操作完成后，SAN 服务提供程序将调用 Win32 **SetEvent** 函数，以指示以前在 **WSPEventSelect** 调用中注册的事件对象。

5.  发出事件对象信号后，开关会调用 SAN 服务提供程序的 [**WSPEnumNetworkEvents**](/previous-versions/windows/hardware/network/ff566284(v=vs.85)) 函数以获取连接操作的结果。

**注意**   交换机通过 SAN 服务提供程序建立连接后，该交换机无法再将 TCP/IP 提供程序用于该连接。 SAN 服务提供程序必须完全实现为建立的连接提供服务所需的所有功能。

 

### <a name="destroying-the-san-socket"></a>销毁 SAN 套接字

如果 SAN 服务提供商的 **WSPConnect** 函数失败，则交换机会调用 san 服务提供商的 [**WSPCloseSocket**](/previous-versions/windows/hardware/network/ff566273(v=vs.85)) 函数来销毁 san 套接字。 然后，交换机会调用 TCP/IP 服务提供程序的 **WSPConnect** 函数，将连接操作转发到 tcp/ip 服务提供程序，除非 SAN 服务提供程序返回以下错误代码之一作为其连接操作的结果：

<a href="" id="wsaeconnreset"></a>**WSAECONNRESET**  
指示没有应用程序在目标地址的指定端口上侦听

<a href="" id="wsaeconnrefused"></a>**WSAECONNREFUSED**  
指示远程应用程序主动拒绝连接请求

<a href="" id="wsaehostunreach"></a>**WSAEHOSTUNREACH**  
指示目标地址不存在

前面的错误代码可保证通过 TCP/IP 建立连接的尝试也会失败。 如果 SAN 服务提供程序无法进行保证，则不能返回这些错误代码之一。 例如，如果 SAN 上不支持 Windows 套接字直通的目标计算机在 SAN 上存在，但只能通过 NDIS 进行通信，则由于通过 TCP/IP 提供程序的连接请求可能成功，因此 SAN 服务提供程序无法将 WSAEHOSTUNREACH 返回为对此目标的 SAN 连接请求失败。 在这种情况下，SAN 服务提供商应返回 WSAETIMEDOUT。

### <a name="session-negotiation"></a>会话协商

交换机通过 SAN 服务提供程序建立连接后，此开关将调用 SAN 服务提供程序的 [**WSPRegisterMemory**](/previous-versions/windows/hardware/network/ff566311(v=vs.85)) extension 函数来预先注册用于接收传入消息的缓冲区数组的内存。 下一步将调用 SAN 服务提供商的 [**WSPRecv**](/previous-versions/windows/hardware/network/ff566309(v=vs.85)) 函数，以发布一个或多个缓冲区来接收来自远程对等方的传入消息数据。 然后，切换器通过交换包含初始流控制信息的一对消息来与远程对等机协商会话。 交换机协商会话后，它将完成应用程序启动的 **WSPConnect** 调用。 然后，应用程序可以开始发送和接收连接的数据。 有关详细信息，请参阅 [接受连接请求](accepting-connection-requests.md)。

通过 SAN 套接字建立连接后，交换机不会调用 SAN 服务提供程序的 **WSPConnect** 函数。 开关在内部处理启动对交换机的 **WSPConnect** 函数的调用以轮询连接请求的应用程序。

 

