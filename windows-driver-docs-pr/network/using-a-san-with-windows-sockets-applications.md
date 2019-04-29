---
title: 将 SAN 与 Windows Sockets 应用程序配合使用
description: 将 SAN 与 Windows Sockets 应用程序配合使用
ms.assetid: 140505dd-2e3c-48b2-94c0-911ea460068c
keywords:
- 系统区域网络 WDK，Windows 套接字应用程序
- SAN WDK，Windows 套接字应用程序
- Windows 套接字应用程序 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e08d778e15989f6ced0e87f310b6569b4791151
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372172"
---
# <a name="using-a-san-with-windows-sockets-applications"></a>将 SAN 与 Windows Sockets 应用程序配合使用





Windows 套接字应用程序可以受益于使用系统区域网络 (SAN)。 这些应用程序可以使用 SAN 传输中大容量形式的数据以及删除直接到 SAN 网络上的数据而不复制在使用一种称为技术的用户内核边界之间[Windows 套接字直接](windows-sockets-direct.md)。 Windows 套接字直接允许这些应用程序以透明方式使用 SAN。

每个 Windows 套接字应用程序，Windows 套接字直接可以：

-   通过直接到 SAN 的 SAN 传送的路由数据流量。

    系统提供 Windows 套接字切换源自 Windows 套接字应用程序直接 SAN NIC 要通过 SAN 网络传输的 SAN 的 Windows 套接字直接路由数据流量的组件。 此开关使用该 SAN 的特定 Windows 套接字服务提供程序传输数据。

-   通过 TCP/IP 通过其他网络传送的路由数据流量。

    若要不用于从 Windows 套接字应用程序的特定 SAN 的数据流量路由，该交换机必须使用 TCP/IP 服务提供程序。 非 SAN 特定的数据流量包括，例如，数据报、 多播和必须进行路由的连接。 然后，非 SAN 特定的数据流量路由通过 TCP/IP 和 NDIS 微型端口驱动程序到 SAN nic。

 

 





