---
title: 创建组件以使用 SAN
description: 创建组件以使用 SAN
keywords:
- 系统区域网络 WDK，创建组件
- SAN WDK，创建组件
- 传输驱动程序 WDK San
- 数据传输 WDK San
- 传输数据 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7426a8c11841738e836eefbe472b99de09c59d9e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794659"
---
# <a name="creating-components-for-using-a-san"></a>创建组件以使用 SAN





Windows 套接字应用程序可以从使用系统区域网络 (SAN) 中获益。 若要使用 SAN，这些应用程序必须有一个 SAN 服务提供程序 DLL 和一个 DLL 的代理驱动程序。

要使用特定的 SAN 来传输数据，还需要为该 SAN 提供可靠的传输。 如果 SAN NIC 硬件中未完全实现可靠传输，则需要为 SAN 使用传输驱动程序。 如果需要，san 传输驱动程序由 SAN NIC 供应商指定，并通过专用接口与其过量的 SAN 代理驱动程序和基础 SAN NIC 通信。

有关实现 SAN 服务提供程序 DLL 及其代理驱动程序的信息，请参阅 [Windows 套接 Direct](windows-sockets-direct.md)。 但请注意，此部分不指定如何编写 SAN 传输驱动程序。

需要一个 NDIS 微型端口驱动程序来传输必须流过除特定 SAN （如以太网、ATM 或其他 SAN）以外的网络的数据。 TCP/IP 使用 NDIS 微型端口驱动程序将数据发送到 SAN NIC，并通过此类网络发送数据。

有关实现微型端口和传输驱动程序的信息，请参阅 *微型端口驱动程序* 和 [TDI 传输及其客户端](/previous-versions/windows/hardware/network/ff565587(v=vs.85))。

 

