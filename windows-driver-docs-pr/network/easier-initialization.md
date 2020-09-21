---
title: 更轻松的初始化
description: 更轻松的初始化
ms.assetid: 34f939fd-2bcc-482b-b877-42cc57bdf59b
keywords:
- NDIS WDK，初始化驱动程序
- 初始化驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7055e2d7f7523e622d0adf959dae8c670a4638d
ms.sourcegitcommit: 366a15d68eb58d01a8ca6de7b982f62ac8b7deaf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90812016"
---
# <a name="easier-initialization"></a>更轻松的初始化





所有 NDIS 6.0 和更高版本的驱动程序都有更新的驱动程序注册接口。 这些 NDIS 接口提供简化的驱动程序注册，并能够将可选服务与所需的服务分开注册。

小型端口驱动程序需要更少的函数调用来注册。 通常，与 NDIS 5 相比，NDIS 6.0 和更高版本的函数接口更为一致。*x* 和更早的接口。 分配的资源还具有用于释放它们的互用功能。

NDIS 6.0 或更高版本中间驱动程序可以注册为微型端口中间驱动程序。 此类驱动程序具有虚拟设备的虚拟小型端口和物理设备的微型端口适配器。 注册为微型端口中间驱动程序可简化创建只绑定到供应商自己的 NIC 的中间驱动程序的过程。 驱动程序可以在其虚拟小型端口和物理微型端口适配器之间通过内部调用传递网络数据、OID 请求和状态指示。

协议驱动程序接收绑定请求中有关基础适配器的大部分信息。 因此，对于在绑定请求中已提供 NDIS 的参数，协议驱动程序不会发送 OID 请求。

若要初始化微型端口适配器，微型端口驱动程序可以接收 OID 请求，这些请求将来自多个单独 OID 请求的信息合并到包含合并信息的较少请求中。

中间驱动程序的专用函数更少，并且更好地使用微型端口驱动程序和协议驱动程序接口。

微型端口驱动程序可以随时读取或写入注册表--而不是在初始化过程中。 例如，当应用程序通过 Windows Management Instrumentation 的 (WMI 请求) ，驱动程序将更改其一个操作参数，驱动程序可以在注册表中记录此更改，使更改在重新启动后保持。

NDIS 提供与总线无关的函数调用，用于读取和写入特定于总线的配置参数。 无论系统中的总线类型如何，驱动程序都可以调用此函数。 这可以确保 NDIS 能够支持未来的总线，而不会添加新的特定于总线的函数。

有关驱动程序初始化的详细信息，请参阅以下部分中的初始化主题：

[编写 NDIS 微型端口驱动程序](./initializing-a-miniport-driver.md)

[编写 NDIS 协议驱动程序](initializing-a-protocol-driver.md)

[NDIS 筛选器驱动程序](ndis-filter-drivers.md)

[编写 NDIS 中间驱动程序](writing-ndis-intermediate-drivers.md)

 

