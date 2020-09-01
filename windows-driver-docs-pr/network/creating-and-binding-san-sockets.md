---
title: 创建和绑定 SAN 套接字
description: 创建和绑定 SAN 套接字
ms.assetid: 0589bd82-40d3-42df-926c-93093fb0617f
keywords:
- SAN 连接设置 WDK，套接字创建和绑定
- SAN 套接字 WDK San
- 随附套接字 WDK San
- 未通过的伴随套接字调用 WDK San
- 绑定配套套接字
- TCP/IP 套接字 WDK San
- SAN 服务提供商 WDK，决定
- 原始套接字 WDK San
- SAN 套接字 WDK，创建
- SAN 套接字 WDK，绑定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ec07a5924f6b7f063ef625b48b4799d14b35360
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214750"
---
# <a name="creating-and-binding-san-sockets"></a>创建和绑定 SAN 套接字





如果 Windows 套接交换机确定它可以通过 SAN 连接而不是通过 TCP/IP 堆栈来路由数据，则它会请求相应的 SAN 服务提供程序为可以传输数据的套接字创建、绑定和设置选项。

SAN 服务提供商创建的套接字与 TCP/IP 服务提供程序在应用程序请求时创建的套接字（来自或传输数据的源） *配套* 。 如果 SAN 服务提供商支持这些选项，则由 SAN 服务提供商创建的 *配套套接字* 与 tcp/ip 服务提供商创建的套接字具有相同的选项。

随附套接字的 IP 地址和 TCP 端口也与 TCP/IP 服务提供商创建的套接字相同。 SAN 数据通过 SAN 服务提供商创建的配套套接字传输，而不是由 TCP/IP 服务提供商创建的套接字传输。 SAN 套接字对应用程序不可见。 从应用程序的角度来看，数据是在其请求为数据传输创建的套接字上传输的。

**注意**   交换机始终使用 TCP/IP 服务提供程序在*原始套接字*上传输数据。 因此，此开关不会请求 SAN 服务提供程序创建原始套接字。

 

下图显示了 Windows 套接交换机如何创建配套套接字的概述。 下面各部分中的顺序说明了如何更详细地创建配套套接字。

![图表概述 windows 套接字交换机如何创建配套套接字](images/apiflow2.png)

### <a name="initiating-creation-of-a-tcpip-socket"></a>启动 TCP/IP 套接字的创建

1.  Windows 套接字交换机接收到由应用程序启动的 **WSPSocket** 调用后，交换机会调用 tcp/ip 提供程序的 **WSPSocket** 函数，请求 tcp/ip 提供程序创建套接字。

2.  Windows 套接交换机将所创建的套接字的描述符返回到应用程序，并将此描述符存储在与套接字关联的专用数据结构中。

    从应用程序的角度来看，TCP/IP 提供程序创建的套接字是用于数据传输的套接字，无论交换机是使用 TCP/IP 服务提供商还是 SAN 服务提供商传输数据。

### <a name="binding-a-tcpip-socket"></a>绑定 TCP/IP 套接字

1.  如果应用程序请求将套接字绑定到特定的网络接口控制器 (NIC) 或通配符 IP 地址 (0.0.0.0) ，则开关接收到 **WSPBind** 调用。 绑定到通配符 IP 地址的套接字可以侦听来自所有 Nic 的传入连接请求。

    **注意**   从 Windows Vista 开始，通配符 IP 地址0.0.0.0 不可用。
    此外，从 Windows Vista 开始，如果 **IPAutoconfigurationEnabled** 注册表项设置为值0，将禁用自动 ip 地址分配，并且不分配 ip 地址。 在这种情况下， **ipconfig** 命令行工具不会显示 IP 地址。 如果将密钥设置为非零值，则会自动分配 IP 地址。 此密钥可位于注册表中的以下路径：

    **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ 当前控制集 \\ 服务 \\ Tcpip \\ 参数 \\ IPAutoconfigurationEnabled**

    **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ 当前控制集 \\ 服务 \\ Tcpip \\ 参数 \\ 接口 \\ *GUID* \\ IPAutoconfigurationEnabled**

     

2.  开关通过调用 TCP/IP 提供程序的 **WSPBind** 函数，将此调用转发到 tcp/ip 服务提供程序。

### <a name="service-provider-determination"></a>服务提供商确定

1.  在应用程序启动对交换机的 **WSPListen** 或 **WSPConnect** 调用后，开关决定是否使用 san 服务提供程序在套接字上传输数据，如 [设置 SAN 连接](setting-up-a-san-connection.md)中所述。

2.  如果交换机确定不能使用 SAN 服务提供程序进行数据传输，则交换机会通过 TCP/IP 服务提供商路由数据传输。

3.  如果交换机选择一个 SAN 服务提供商来服务应用程序的套接字，则交换机会调用 SAN 服务提供商的 [**WSPSocket**](/previous-versions/windows/hardware/network/ff566319(v=vs.85)) 函数来创建配套套接字。

### <a name="initiating-creation-of-a-companion-socket"></a>开始创建配套套接字

1.  SAN 服务提供程序的 **WSPSocket** 函数初始化内部数据结构，其中存储了有关随附套接字的信息。

2.  接下来，SAN 服务提供程序的 **WSPSocket** 函数必须调用 **WPUCreateSocketHandle** 函数，以从开关获取套接字说明符。

3.  SAN 服务提供程序必须将交换机的套接字描述符存储在随附套接字的内部数据结构中，并且必须为随附套接字返回其自己的描述符才能完成 **WSPSocket** 调用。 SAN 服务提供程序返回的套接字描述符可以是任何有意义的值，例如指向私有数据结构的指针。

4.  若要在套接字上执行操作，开关会将 SAN 服务提供程序返回的套接字描述符提供给 SAN 服务提供程序的适当功能。 同样，如果 SAN 服务提供商执行以下任何调用，则 SAN 服务提供程序必须提供从 **WPUCreateSocketHandle** 调用中的交换机获取的套接字描述符：

    **WPUQuerySocketHandleContext**

    **WPUCloseSocketHandle**

    **WPUCompleteOverlappedRequest**

### <a name="binding-a-companion-socket"></a>绑定配套套接字

1.  如果 SAN 服务提供商的 **WSPSocket** 函数成功完成，则交换机会立即调用 SAN 服务提供商的 [**WSPBind**](/previous-versions/windows/hardware/network/ff566268(v=vs.85)) 函数，将本地 IP 地址和 TCP 端口分配给套接字。

2.  交换机将相同的 IP 地址和 TCP 端口分配给 SAN 套接字，就像分配给 TCP/IP 提供程序创建的套接字一样。 SAN 服务提供程序必须将此 TCP/IP 地址转换为其本机格式。

3.  交换机提供完全限定的 IP 地址和 TCP 端口 (也就是说，非零值) 到 SAN 服务提供程序的 **WSPBind** 函数，除非应用程序请求侦听来自所有 nic 的传入连接。 在稍后的示例中，交换机将通配符 IP 地址提供给 SAN 服务提供商的 **WSPBind** 函数。

### <a name="setting-options-for-a-companion-socket"></a>为配套套接字设置选项

-   如果应用程序指定了任何套接字选项，则交换机会存储这些选项。 创建 SAN 套接字后，交换机会为应用程序指定的每个受支持选项调用 SAN 服务提供程序的 [**WSPSetSockOpt**](/previous-versions/windows/hardware/network/ff566318(v=vs.85)) 函数，以便为 SAN 套接字立即设置这些选项。

### <a name="failing-a-companion-socket-call"></a>未能通过伴随套接字呼叫

-   如果 SAN 服务提供程序在上述任何调用 **WSPSocket**、 **WSPBind**或 **WSPSetSockOpt** 函数时失败，则该开关将调用 san 服务提供程序的 [**WSPCloseSocket**](/previous-versions/windows/hardware/network/ff566273(v=vs.85)) 函数以销毁 san 套接字。 然后，交换机使用 TCP/IP 提供程序来继续处理应用程序套接字。 请注意，在交换机使用 SAN 服务提供程序建立连接后，交换机无法使用 TCP/IP 提供程序来处理应用程序的套接字。 在这种情况下，开关会将相应的错误返回到应用程序。

### <a name="connecting-the-companion-socket"></a>连接配套套接字

-   交换机设置了配套套接字后，交换机将为 SAN 服务提供程序调用 **WSPListen** 或 **WSPConnect** 函数，以执行导致 SAN 服务提供程序最初设置套接字的操作。 例如，如果某个应用程序最初请求侦听传入连接，则该开关将调用 SAN 服务提供程序的 [**WSPListen**](/previous-versions/windows/hardware/network/ff566297(v=vs.85)) 函数。

 

