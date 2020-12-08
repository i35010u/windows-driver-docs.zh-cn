---
title: 侦听 SAN 上的连接
description: 侦听 SAN 上的连接
keywords:
- SAN 连接设置 WDK，侦听连接
- 侦听操作 WDK San
- 拒绝 SAN 连接请求
- 远程对等连接 refusals WDK SANs
- 非阻止模式 WDK San
- WSPListen
- SAN 套接字 WDK，侦听连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5fdd865df0150718d73a469b5f0c64bd3e080bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792175"
---
# <a name="listening-for-connections-on-a-san"></a>侦听 SAN 上的连接





下图显示了 Windows 套接交换机如何设置要确认和排队的 SAN 套接字的概述，即侦听来自远程对等方的传入连接请求。 以下主题更详细地介绍了侦听过程。

![图示 windows 套接交换机如何设置 san 套接字以确认和排队来自远程对等方的传入连接请求](images/apiflow4.png)

当 Windows 套接字交换机收到应用程序启动的 **WSPListen** 调用时，此开关将首先调用 tcp/ip 提供程序的 **WSPListen** 函数，以将 tcp/ip 提供程序的套接字设置为确认并将传入连接请求排队。 如果应用程序的套接字绑定到 SAN NIC 的 IP 地址或通配符 IP 地址，则交换机还会使用相应的 SAN 服务提供程序来创建和绑定其他套接字。 有关详细信息，请参阅 [创建和绑定 SAN 套接字](creating-and-binding-san-sockets.md)。

### <a name="listening-for-incoming-connection-requests"></a>侦听传入连接请求

请求 SAN 服务提供程序创建和绑定 SAN 套接字后，交换机将调用 SAN 服务提供程序的 [**WSPListen**](/previous-versions/windows/hardware/network/ff566297(v=vs.85)) 函数，以使 san 套接字侦听传入连接，并指定 san 服务提供商可以排队的传入连接请求数的限制。

### <a name="setting-up-to-accept-incoming-connections"></a>设置以接受传入连接

此开关仅在非阻止模式下接受传入连接。 开关调用 SAN 服务提供程序的 [**WSPEventSelect**](/previous-versions/windows/hardware/network/ff566287(v=vs.85)) 函数，使套接字处于非阻止模式并请求传入连接事件的通知。 在此调用中，开关传递 FD \_ ACCEPT 代码和要与该代码相关联的事件对象。 在 SAN 服务提供程序在其套接字上收到以前建立用于侦听的连接请求后，SAN 服务提供程序将调用 Win32 **SetEvent** 函数来发出关联事件对象的信号。 开关侦听专用线程中的传入连接事件，并在事件对象终止后接受或拒绝连接。 有关详细信息，请参阅 [接受连接请求](accepting-connection-requests.md)。

### <a name="indicating-refusal-of-a-connection-request-to-a-remote-peer"></a>指示拒绝到远程对等方的连接请求

如果连接请求到达，且 SAN 服务提供程序的连接请求积压（backlog）已满，则 SAN 服务提供程序应立即向远程对等机指出拒绝连接请求。 在这种情况下，SAN 服务提供程序不会向事件对象发出信号，通知交换机接受或拒绝连接请求。 远程对等方上的 SAN 服务提供程序必须使用 WSAECONNREFUSED 错误代码将 **WSPConnect** 调用启动的连接操作失败。

 

