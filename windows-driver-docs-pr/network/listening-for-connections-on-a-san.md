---
title: 侦听在 SAN 上的连接
description: 侦听在 SAN 上的连接
ms.assetid: 7e430bda-74f5-4a1a-90f0-3b2e44fb25a3
keywords:
- SAN 连接安装 WDK，侦听连接
- 侦听操作 WDK San
- 拒绝 SAN 连接请求
- 远程对等连接 refusals WDK San
- 阻止模式下 WDK San
- WSPListen
- SAN 套接字 WDK，侦听连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b895c4922ed64900ee7eeeaf1181c41377a1ea49
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544956"
---
# <a name="listening-for-connections-on-a-san"></a>侦听在 SAN 上的连接





下图显示了 Windows 套接字如何切换集的概述，SAN 套接字以确认和队列-即，侦听-远程对等方的传入连接请求。 后面的主题描述更详细地侦听的进程。

![关系图概述 windows 套接字如何切换设置 san 套接字以确认并从远程对等方的传入连接请求进行排队](images/apiflow4.png)

Windows 套接字时切换接收**WSPListen**由应用程序中，始终开关启动的调用将调用 TCP/IP 提供程序的**WSPListen**函数首先设置 TCP/IP 提供程序套接字以确认并对传入连接请求进行排队。 如果应用程序的套接字绑定到 SAN NIC 的 IP 地址或通配符 IP 地址，该交换机还使用适当的 SAN 服务提供程序来创建和绑定其他套接字。 有关详细信息，请参阅[创建和绑定 SAN 套接字](creating-and-binding-san-sockets.md)。

### <a name="listening-for-incoming-connection-requests"></a>侦听传入连接请求

请求一个 SAN 服务提供程序来创建和绑定 SAN 套接字后，将调用该交换机[ **WSPListen** ](https://msdn.microsoft.com/library/windows/hardware/ff566297) SAN 服务提供程序会导致 SAN 套接字来侦听传入连接的函数和入站连接的数量指定的限制 SAN 服务提供商的请求可以排入队列。

### <a name="setting-up-to-accept-incoming-connections"></a>设置为接受传入连接

开关接受传入连接仅在非阻止性模式下。 此开关调用 SAN 服务提供商[ **WSPEventSelect** ](https://msdn.microsoft.com/library/windows/hardware/ff566287)函数将套接字置于阻止模式下，并请求的传入连接事件的通知。 在此调用，此开关传递 FD\_接受代码和要与该代码相关联的事件对象。 SAN 服务提供商的 SAN 服务提供程序收到侦听以前建立了其套接字上的连接请求后，调用 Win32 **SetEvent**函数发出信号的关联的事件对象。 开关的专用线程中的传入连接事件侦听和接受或拒绝连接事件对象信号后。 有关详细信息，请参阅[接受连接请求](accepting-connection-requests.md)。

### <a name="indicating-refusal-of-a-connection-request-to-a-remote-peer"></a>指示拒绝连接请求发送到远程对等方的消息

如果收到连接请求和 SAN 服务提供商的积压工作的连接请求已满，SAN 服务提供程序应立即向指示远程对等方，它将拒绝连接请求。 在这种情况下，SAN 服务提供商不表示要通知开关来接受或拒绝连接请求的事件对象。 远程对等方上的 SAN 服务提供程序必须则失败由启动其连接操作**WSPConnect** WSAECONNREFUSED 错误代码调用。

 

 





