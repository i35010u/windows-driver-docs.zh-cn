---
title: 更轻松的初始化
description: 更轻松的初始化
ms.assetid: 34f939fd-2bcc-482b-b877-42cc57bdf59b
keywords:
- NDIS WDK，初始化驱动程序
- 初始化驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 035e4482ee4724d25b5718290883a9e66038a3cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372644"
---
# <a name="easier-initialization"></a>更轻松的初始化





所有 NDIS 6.0 和更高版本的驱动程序已都更新驱动程序注册接口。 这些 NDIS 接口提供简化的驱动程序注册和注册独立于所需的服务的可选服务的功能。

微型端口驱动程序需要更少的函数调用以注册。 一般情况下，NDIS 6.0 和更高版本的函数接口是与 NDIS 5 相比更一致。*x*和早期的接口。 分配的资源还具有一个相应的函数来释放它们。

NDIS 6.0 或更高版本的中间驱动程序可以将注册为中间微型端口驱动程序。 此类驱动程序包含两个虚拟设备虚拟微型端口和物理设备的微型端口适配器。 注册为中间微型端口驱动程序简化了创建仅绑定到供应商自己的 NIC 的中间驱动程序 驱动程序可以传递其虚拟微型端口与物理微型端口适配器与内部调用之间的网络数据、 OID 请求和状态指示。

协议驱动程序绑定请求中收到大部分基础适配器有关的信息。 因此，协议驱动程序不发送绑定请求在 NDIS 已提供的参数的 OID 请求。

若要初始化的微型端口适配器，微型端口驱动程序可以接收这些信息组合来自多个单独的 OID 请求到较少的请求包含组合后的信息的 OID 请求。

中间驱动程序具有较少的专用的函数和更好地利用微型端口驱动程序和协议驱动程序接口。

微型端口驱动程序可以读取，或在任何时间--不只是在初始化期间写入注册表。 例如，当应用程序请求了其操作的参数之一，更改驱动程序通过 Windows Management Instrumentation (WMI)，该驱动程序可以记录此更改在注册表中，以便更改在重新启动后仍然存在。

NDIS 提供独立于总线的函数调用，用于读取和写入特定于总线的配置参数。 驱动程序可以调用此函数而不考虑总线类型系统中。 这可确保 NDIS 将能够支持未来总线，而无需添加新的特定于总线的函数。

有关驱动程序初始化的详细信息，请参阅以下各节中的初始化主题：

[编写 NDIS 微型端口驱动程序](writing-ndis-miniport-drivers.md)

[编写 NDIS 协议驱动程序](writing-ndis-protocol-drivers.md)

[NDIS 筛选器驱动程序](ndis-filter-drivers.md)

[编写 NDIS 中间驱动程序](writing-ndis-intermediate-drivers.md)

 

 





