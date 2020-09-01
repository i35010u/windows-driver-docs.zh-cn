---
title: 阻止调用 SAN
description: 阻止调用 SAN
ms.assetid: 93be861c-4cf1-48ea-ac69-a4a171ca9052
keywords:
- 阻止调用 WDK San
- Windows 套接字直接 WDK，阻止呼叫
- SAN 阻塞调用 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe9717417d35417b5512f56e98b541f8ae6e54f8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206473"
---
# <a name="blocking-calls-for-a-san"></a>阻止调用 SAN





Windows 套接交换机处理阻止调用，并在内部取消此类调用，或将其转发给 TCP/IP 服务提供商。 对于 SAN 服务提供程序，开关从不调用 **WSPCancelBlockingCall** 函数来取消正在进行的阻止请求。 因此，不需要 SAN 服务提供商即可实现 **WSPCancelBlockingCall** 函数。

开关按以下方式处理以下阻塞请求和相应的取消：

-   当应用程序请求将 SAN 套接字连接到处于阻止模式的特定目标地址时，交换机会接收到阻止 **WSPConnect** 调用。 交换机会在非阻止模式下将连接请求转发到相应的 SAN 服务提供商的 [**WSPConnect**](/previous-versions/windows/hardware/network/ff566275(v=vs.85)) 函数。 如果开关由于某种原因而必须取消此连接请求，它将调用 SAN 服务提供程序的 [**WSPCloseSocket**](/previous-versions/windows/hardware/network/ff566273(v=vs.85)) 函数。 SAN 服务提供商必须立即中止套接字的连接请求和释放资源。

-   当交换机收到由应用程序启动的阻止请求以在 SAN 套接字上执行数据传输操作时，它会将数据传输请求以重叠方式转发给相应的 SAN 服务提供程序， (非阻止性) 。 例如，如果交换机接收到 (阻止) **WSPSend** 调用的同步，则它将以重叠 (非阻止) 方式调用相应的 SAN 服务提供程序的 [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85)) 函数。 如果应用程序稍后取消数据传输操作，并且交换机控制了应用程序的缓冲区，则该开关将以失败状态完成应用程序的请求。 如果在未完成的 RDMA 操作中涉及应用程序的缓冲区，则开关将等待操作完成。 如果 RDMA 传输时间太长而无法完成，则交换机将调用相应的 SAN 服务提供程序的 **WSPCloseSocket** 函数以异常的方式关闭连接，从而强制完成。

**注意**   如果应用程序取消阻止调用，则不会依赖于被保留的连接。 取消阻塞请求后，只能保证 **WSPCloseSocket** 调用在套接字上成功。 有关详细信息，请参阅中的 Windows 套接字 SPI 文档 Microsoft Windows SDK。

 

 

