---
title: 创建和绑定 SAN 套接字
description: 创建和绑定 SAN 套接字
ms.assetid: 0589bd82-40d3-42df-926c-93093fb0617f
keywords:
- SAN 连接安装 WDK，套接字的创建和绑定
- SAN 套接字 WDK San
- 随附套接字 WDK San
- 失败的配套套接字调用 WDK San
- 绑定随附套接字
- TCP/IP 套接字 WDK San
- SAN 服务提供商 WDK，判断
- 原始套接字 WDK San
- SAN 套接字 WDK，创建
- SAN 套接字 WDK 绑定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a536797eb2f860c395d5a2997f344eda8f5de4f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357368"
---
# <a name="creating-and-binding-san-sockets"></a>创建和绑定 SAN 套接字





如果 Windows 套接字交换机确定它可以将数据通过 SAN 连接而不是 TCP/IP 堆栈通过路由，它会请求相应的 SAN 服务提供程序来创建，将绑定，并设置可以在其传输数据的套接字选项。

是 SAN 服务提供程序创建的套接字*配套*到 TCP/IP 服务提供程序在应用程序，从或向其传输数据的请求时创建的套接字。 *配套套接字*创建 san 服务提供程序具有相同的选项，如 TCP/IP 服务提供程序，如果 SAN 服务提供商创建的套接字支持这些选项。

随附套接字也具有相同的 IP 地址和 TCP 端口已通过 TCP/IP 服务提供商的套接字。 通过创建的 SAN 服务提供程序而不是 TCP/IP 服务提供程序创建的套接字的配套套接字传输 SAN 数据。 SAN 套接字不到应用程序可见。 从应用程序的角度来看，它请求的数据传输要创建的套接字传输数据。

**请注意**  开关始终使用 TCP/IP 服务提供商通过传输数据*原始套接字*。 开关因此永远不会请求 SAN 服务提供商合作创建原始套接字。

 

下图显示的 Windows 套接字如何切换概述创建随附套接字。 以下各节中的序列描述了更详细地创建随附套接字。

![windows 套接字如何切换的关系图概述创建随附套接字](images/apiflow2.png)

### <a name="initiating-creation-of-a-tcpip-socket"></a>启动创建 TCP/IP 套接字

1.  Windows 套接字后交换机接收**WSPSocket**由应用程序，此开关启动的调用将调用 TCP/IP 提供程序的**WSPSocket**函数请求 TCP/IP 提供商合作创建套接字。

2.  Windows 套接字开关创建套接字描述符返回到应用程序，并将此描述符存储在与套接字关联的专用数据结构。

    从应用程序的角度来看，TCP/IP 提供程序创建的套接字是用于数据传输，是否开关使用 TCP/IP 服务提供商或 SAN 服务提供商将数据传输的套接字。

### <a name="binding-a-tcpip-socket"></a>绑定 TCP/IP 套接字

1.  开关接收**WSPBind**调用如果应用程序请求可将套接字绑定到特定网络接口控制器 (NIC) 或通配符 IP 地址 (0.0.0.0)。 套接字绑定到的通配符 IP 地址可以侦听来自所有 Nic 的传入连接请求。

    **请注意**  从 Windows Vista 开始，通配符 IP 地址 0.0.0.0 不可用。
    如果还从 Windows Vista **IPAutoconfigurationEnabled**注册表项设置为值为 0，禁用自动 IP 地址分配，和任何 IP 地址分配。 在这种情况下， **ipconfig**命令行工具将不会显示一个 IP 地址。 如果项设置为非零值，自动分配 IP 地址。 此密钥也可位于注册表中的以下路径：

    **HKEY\_本地\_MACHINE\\系统\\当前控件集\\Services\\Tcpip\\参数\\IPAutoconfigurationEnabled**

    **HKEY\_本地\_MACHINE\\系统\\当前控件集\\Services\\Tcpip\\参数\\接口\\*GUID*\\IPAutoconfigurationEnabled**

     

2.  交换机将通过调用 TCP/IP 提供程序的转发对 TCP/IP 服务提供程序的此调用**WSPBind**函数。

### <a name="service-provider-determination"></a>服务提供程序确定

1.  开关确定是否使用 SAN 服务提供商的套接字上的数据传输，该应用程序启动后**WSPListen**或**WSPConnect**开关，如中所述调用[设置 SAN 连接](setting-up-a-san-connection.md)。

2.  如果交换机确定它不能使用相应的数据传输 SAN 服务提供程序，此开关将路由通过 TCP/IP 服务提供商的数据传输。

3.  如果开关选择 SAN 服务提供商，以服务应用程序的套接字，此开关调用 SAN 服务提供商的[ **WSPSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566319)函数来创建随附套接字。

### <a name="initiating-creation-of-a-companion-socket"></a>启动创建随附套接字

1.  SAN 服务提供商**WSPSocket**函数初始化内部数据结构，它将在其中存储随附套接字有关的信息。

2.  SAN 服务提供商**WSPSocket**接下来必须调用函数**WPUCreateSocketHandle**函数获取从交换机的套接字描述符。

3.  SAN 服务提供商必须存储交换机的套接字描述符配套套接字其内部数据结构中，并且必须返回要完成的配套套接字自己描述符**WSPSocket**调用。 SAN 服务提供程序返回的套接字描述符可以是任何有意义的值，例如指向专用数据结构的指针。

4.  若要执行的套接字上的操作，该交换机提供给 SAN 服务提供程序的适当的函数返回的 SAN 服务提供商的套接字描述符。 同样，SAN 服务提供商必须提供已获取在交换机中的套接字描述符**WPUCreateSocketHandle**如果 SAN 服务提供程序会调用以下任何调用：

    **WPUQuerySocketHandleContext**

    **WPUCloseSocketHandle**

    **WPUCompleteOverlappedRequest**

### <a name="binding-a-companion-socket"></a>绑定随附套接字

1.  如果 SAN 服务提供商**WSPSocket**函数成功完成，此开关立即调用 SAN 服务提供商[ **WSPBind** ](https://msdn.microsoft.com/library/windows/hardware/ff566268)函数将分配本地 IP 地址和 TCP 端口套接字。

2.  开关会将相同的 IP 地址和 TCP 端口分配给 SAN 套接字已分配给已通过 TCP/IP 提供程序的套接字。 SAN 服务提供程序必须将此 TCP/IP 地址转换为其本机格式。

3.  切换到 SAN 服务提供商提供完全限定的 IP 地址和 TCP 端口 （即，非零值） **WSPBind**作用，除非应用程序请求以侦听来自所有 Nic 的传入连接。 在更高版本的情况下，该交换机提供 SAN 服务提供商的通配符 IP 地址**WSPBind**函数。

### <a name="setting-options-for-a-companion-socket"></a>设置助理套接字选项

-   如果应用程序指定的任何套接字选项，此开关将存储这些选项。 创建后 SAN 套接字，此开关调用 SAN 服务提供商[ **WSPSetSockOpt** ](https://msdn.microsoft.com/library/windows/hardware/ff566318)由应用程序可以立即设置这些选项指定的每个受支持选项的函数SAN 套接字。

### <a name="failing-a-companion-socket-call"></a>失败的配套套接字调用

-   如果 SAN 服务提供程序没有通过任何对前面的调用其**WSPSocket**， **WSPBind**，或**WSPSetSockOpt**函数，此开关调用 SAN 服务提供商[**WSPCloseSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566273)函数来销毁 SAN 套接字。 此开关使用 TCP/IP 提供程序可以继续响应应用程序套接字。 请注意，交换机建立使用 SAN 服务提供程序的连接后，此开关不能用于 TCP/IP 提供程序服务应用程序的套接字。 在这种情况下，切换到应用程序返回相应的错误。

### <a name="connecting-the-companion-socket"></a>连接的配套套接字

-   切换开关设置助理套接字后，调用任一**WSPListen**或**WSPConnect**函数 SAN 服务提供商来执行该操作导致的 SAN 服务提供程序最初设置套接字。 例如，如果应用程序最初请求来侦听传入连接，该交换机调用 SAN 服务提供商[ **WSPListen** ](https://msdn.microsoft.com/library/windows/hardware/ff566297)函数。

 

 





