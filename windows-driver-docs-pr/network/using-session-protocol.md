---
title: 使用会话协议
description: 使用会话协议
keywords:
- 会话协议 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12e5289c9e4419b1476d666d7e62a6a533f82f8c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803493"
---
# <a name="using-session-protocol"></a>使用会话协议





Windows 套接字交换机使用其会话协议在 SAN 连接上传输数据。 如果交换机传输的数据量较少，则会在控制消息中传输数据。 每个控制消息都包含一个标头和一个可选的应用程序数据负载。 如果交换机传输大量数据，它将使用 RDMA 操作传输该数据。

本部分介绍如何设置和执行数据传输。

**注意**  根据加载交换机的应用程序的行为，交换机会优化其会话协议以降低传输应用程序数据所需的开销。

 

本部分还提供了有关交换机的会话协议如何执行数据传输的示例。 但是，这些示例不包括对这些操作的明确说明。

### <a name="setting-up-a-data-transfer"></a>设置数据传输

开关为每个连接的套接字分配控制消息缓冲区池。 然后，此开关调用 SAN 服务提供程序的 [**WSPRegisterMemory**](/previous-versions/windows/hardware/network/ff566311(v=vs.85)) 函数，将这些消息缓冲区注册到物理内存区域。 调用 SAN 服务提供程序的 [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85)) 函数时，开关使用部分缓冲池将流控制信息发送到远程对等方。 开关使用池的其他部分来发布消息缓冲区，以便在调用 SAN 服务提供程序的 [**WSPRecv**](/previous-versions/windows/hardware/network/ff566309(v=vs.85)) 函数时从远程对等方接收流控制信息。 开关接收控制消息后，它会立即使用它们。 使用控制消息后，开关调用 SAN 服务提供程序的 **WSPRecv** 函数，并传递接收缓冲区以再次发布它们，以便它们可以接收来自远程对等方的其他控制消息。

### <a name="transferring-application-data"></a>传输应用程序数据

数据传输的大小会影响交换机处理数据传输操作的方式。

如果应用程序请求发送少量数据，则交换机会按在 [SAN 上发送紧急数据](sending-urgent-data-on-a-san.md)中所述传输该数据。

如果应用程序请求发送大量数据，则 switch 会将数据的初始部分复制到用于发送的控制消息缓冲区。 此控制消息的标头包含指定应用程序数据量的信息。 然后，交换机调用 SAN 服务提供商的 [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85)) 函数，将此控制消息发送到 san 套接字的远程对等方。

交换机如何完成应用程序数据的传输取决于服务提供商是否支持 [**WSPRdmaRead**](/previous-versions/windows/hardware/network/ff566304(v=vs.85)) 函数。

### <a name="data-transfer-to-a-provider-that-supports-the-wsprdmaread-function"></a>数据传输支持 WSPRdmaRead 函数的访问接口

下图显示了当远程对等机上的 SAN 服务提供商支持 WSPRdmaRead 功能时，交换机如何完成应用程序数据传输的概述。 下面的顺序说明了如何更详细地传输应用程序数据。

![远程对等机支持 wsprdmaread](images/wsprdmaread.png)

### <a name="to-transfer-data-when-the-remote-peer-supports-wsprdmaread"></a>当远程对等机支持 WSPRdmaRead 时传输数据

-   本地交换机必须调用 SAN 服务提供商的 [**WSPRegisterRdmaMemory**](/previous-versions/windows/hardware/network/ff566313(v=vs.85)) 函数来注册 RDMA 内存以进行读访问。 在这种情况下，消息缓冲区的控制标头还会标识包含应用程序剩余数据的 RDMA 内存的描述符。
-   然后，远程对等节点上的开关将调用 [**WSPRdmaRead**](/previous-versions/windows/hardware/network/ff566304(v=vs.85)) ，以将应用程序数据从 RDMA 内存传输到接收缓冲区，这些缓冲区之前已向 [**WSPRegisterMemory**](/previous-versions/windows/hardware/network/ff566311(v=vs.85)) 调用注册了远程对等方。 SAN 服务提供程序在后台传输缓冲数据。 如果这样做，则在 SAN 服务提供程序发送缓冲的数据时，一次不会发布多个 send 发送其他发送请求的应用程序。
-   然后，位于远程对等端的开关调用 [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85)) 将控制消息发送到本地开关，以指示传输已完成。
-   本地开关调用 [**WSPDeregisterRdmaMemory**](/previous-versions/windows/hardware/network/ff566281(v=vs.85)) 函数以释放 RDMA 内存。
-   本地开关完成了应用程序的发送请求。 如果切换无法为应用程序的数据缓冲区注册内存，或者如果无法完全分配临时内存，它将使用 **WSAENOBUFS** 错误代码完成应用程序的发送请求。

### <a name="data-transfer-to-a-provider-that-does-not-support-the-wsprdmaread-function"></a>数据传输到不支持 WSPRdmaRead 函数的访问接口

下图显示了当远程对等机上的 SAN 服务提供商不支持 [**WSPRdmaRead**](/previous-versions/windows/hardware/network/ff566304(v=vs.85)) 函数时，交换机如何完成应用程序数据传输。 下面的顺序说明了如何更详细地传输应用程序数据。

![远程对等方不支持 wsprdmaread](images/wsprdmaread2.png)

### <a name="to-transfer-data-when-the-remote-peer-does-not-support-wsprdmaread"></a>当远程对等节点不支持 WSPRdmaRead 时传输数据

-   远程对等机上的开关调用 [**WSPRegisterRdmaMemory**](/previous-versions/windows/hardware/network/ff566313(v=vs.85)) 来注册 RDMA 内存以进行写访问。
-   然后，位于远程对等端的开关调用 [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85)) ，以将控制消息发送到本地开关，该开关指示本地交换机可以写入的 RDMA 内存的位置。
-   本地开关调用 [**WSPRdmaWrite**](/previous-versions/windows/hardware/network/ff566306(v=vs.85)) 函数，将应用程序数据传输到 RDMA 内存。 SAN 服务提供程序在后台传输缓冲数据。 如果这样做，则在 SAN 服务提供程序发送缓冲的数据时，一次不会发布多个 send 发送其他发送请求的应用程序。
-   本地开关调用 [**WSPGetOverlappedResult**](/previous-versions/windows/hardware/network/ff566288(v=vs.85)) 函数来获取传输结果。 有关详细信息，请参阅 " [完成数据传输请求](completing-data-transfer-requests.md)"。
-   本地开关调用 [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85)) 将控制消息发送到远程对等方，以指示传输已完成。
-   远程对等机上的开关调用 [**WSPDeregisterRdmaMemory**](/previous-versions/windows/hardware/network/ff566281(v=vs.85)) 来释放 RDMA 内存。
-   本地开关完成了应用程序的发送请求。 如果切换无法为应用程序的数据缓冲区注册内存，或者无法分配临时内存，它将使用 **WSAENOBUFS** 错误代码完成应用程序的发送请求。

## <a name="related-topics"></a>相关主题


[在 SAN 上传输数据](transferring-data-on-a-san.md)

 

