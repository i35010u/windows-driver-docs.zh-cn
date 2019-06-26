---
title: 阻止调用 SAN
description: 阻止调用 SAN
ms.assetid: 93be861c-4cf1-48ea-ac69-a4a171ca9052
keywords:
- 阻止调用 WDK San
- Windows 套接字直接 WDK，阻止调用
- SAN 阻塞调用 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eb01febf3b6919e9945f8436b8c8579f93f09c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354632"
---
# <a name="blocking-calls-for-a-san"></a>阻止调用 SAN





Windows 套接字切换阻塞调用的句柄，并在内部调用此类取消，或将其转发到 TCP/IP 服务提供程序。 永远不会调用该交换机**WSPCancelBlockingCall** SAN 服务提供程序来取消正在进行中的阻塞请求的函数。 因此，SAN 服务提供程序不需要实现**WSPCancelBlockingCall**函数。

交换机处理以下阻塞请求和相应取消以下方面：

-   此开关时应用程序请求 SAN 套接字连接到特定的目标地址在阻止模式下，接收阻塞**WSPConnect**调用。 此开关将在阻止模式下的连接请求转发到相应 SAN 服务提供商[ **WSPConnect** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566275(v=vs.85))函数。 如果该交换机必须出于某种原因取消此连接请求，则会调用 SAN 服务提供商[ **WSPCloseSocket** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566273(v=vs.85))函数。 SAN 服务提供商必须立即中止连接请求，并释放套接字的资源。

-   当交换机收到的阻塞请求的应用程序以执行数据传输操作中的 SAN 套接字上启动时，它将相应 SAN 服务提供程序 （非阻塞） 重叠的方式转发数据传输请求。 例如，如果交换机接收同步 （阻塞） **WSPSend**调用时，它会调用相应 SAN 服务提供商[ **WSPSend** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566316(v=vs.85))在重叠 （函数非阻止性） 的方式。 如果应用程序更高版本将取消数据传输操作，并且该交换机有控制的应用程序的缓冲区，交换机完成失败状态的应用程序的请求。 如果未完成的 RDMA 操作中涉及的应用程序的缓冲区，则该交换机等待操作完成。 如果 RDMA 传输时间太长时间才能完成，此开关调用相应 SAN 服务提供商**WSPCloseSocket**函数来以放弃性方式，从而强制完成关闭连接。

**请注意**  如果应用程序取消阻塞调用，则它不能依赖于保留的连接。 仅**WSPCloseSocket**调用可确保在套接字上的阻塞请求取消后成功。 有关详细信息，请参阅 Microsoft Windows SDK 中的 Windows 套接字 SPI 文档。

 

 

 





