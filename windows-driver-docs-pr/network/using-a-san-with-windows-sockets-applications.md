---
title: 将 SAN 与 Windows Sockets 应用程序配合使用
description: 将 SAN 与 Windows Sockets 应用程序配合使用
keywords:
- 系统区域网络 WDK，Windows 套接字应用程序
- SAN WDK，Windows 套接字应用程序
- Windows 套接字应用程序 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1791bf5baced215af2b0bd9d00c7e7331345c6d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790399"
---
# <a name="using-a-san-with-windows-sockets-applications"></a>将 SAN 与 Windows Sockets 应用程序配合使用





Windows 套接字应用程序可以从使用系统区域网络 (SAN) 中获益。 这些应用程序可以使用 SAN 以批量形式传输数据并将数据直接拖到 SAN 网络，而无需使用称为 [Windows Socket Direct](windows-sockets-direct.md)的技术跨用户内核边界进行复制。 Windows 套接 Direct 允许这些应用程序以透明方式使用 SAN。

对于每个 Windows 套接字应用程序，Windows 套接字直通可以：

-   将流经 SAN 的流量直接路由到 SAN。

    Windows 套接字的系统提供的 Windows 套接字交换机组件会直接将来自 Windows 套接字应用程序的 SAN 的数据流量路由到 SAN NIC，以便通过 SAN 网络进行传输。 交换机使用该 SAN 的特定 Windows 套接字服务提供程序来传输数据。

-   通过 TCP/IP 路由通过其他网络流动的流量。

    若要从 Windows 套接字应用程序路由非特定 SAN 的数据流量，该交换机必须使用 TCP/IP 服务提供程序。 非 SAN 特定的数据流量包括必须路由的数据报、多播和连接。 然后，将通过 TCP/IP 和 NDIS 微型端口驱动程序将非 SAN 特定的数据流量路由到 SAN NIC。

 

 





