---
title: NDPROXY 概述
description: NDPROXY 概述
ms.assetid: 98d01249-8a6d-42b3-a91c-811352c8b638
keywords:
- NDPROXY WDK 网络
- NDISWAN WDK 网络
- 体系结构 WDK WAN，NDPROXY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 691c85252f83e6ace065ebc1680a6a627ee60093
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210163"
---
# <a name="ndproxy-overview"></a>NDPROXY 概述

**注意**   如果你正在阅读本页，因为 Microsoft 安全公告27年11月 2013 [ (2914486) ](/security-updates/SecurityAdvisories/2014/2914486)影响 Windows XP 和 windows Server 2003，你可能会发现此可信计算[博客文章](https://msrc-blog.microsoft.com/2013/11/27/microsoft-releases-security-advisory-2914486/)有帮助。

NDPROXY 是系统提供的驱动程序，可将 WAN 微型端口驱动程序、呼叫管理器和微型端口呼叫管理器) 的 NDISWAN 和 CoNDIS WAN (驱动程序连接到 TAPI 服务。 本主题介绍在 [支持 Telephonic 服务的 CONDIS WAN 操作](./condis-wan-operations-that-support-telephonic-services.md)中进一步记录的 NDPROXY 操作。

下图显示了 NDPROXY 如何与 RAS 体系结构中的其他组件进行交互。

![说明 ndproxy 如何与 ras 体系结构中的其他组件进行交互的关系图](images/ndproxy.png)

NDPROXY 为 CoNDIS WAN (SPI) 提供服务提供程序接口的内核模式组件。 支持 TAPI 的应用程序会发出用户模式 TAPI 请求，TAPI 服务会将这些请求路由到 NDPTSP。 NDPTSP 将用户模式 TAPI 服务请求转换为内核模式 SPI 请求，并将 SPI 请求传递到 NDPROXY。

NDPROXY 通过 NDISWAN 驱动程序和以下内容之一进行 NDIS 通信：

- 使用单独的调用管理器的微型端口驱动程序

-  (MCM 的集成微型端口呼叫管理器) 

无论配置如何，小型端口驱动程序接口和 NDISWAN 和 NDPROXY 的调用管理器接口都是相同的。

**注意**   如果需要支持多个硬件平台，则可以在单独的调用管理器中使用微型端口驱动程序。 在这种情况下，可以结合使用同一调用管理器和多个微型端口驱动程序来简化开发。

以下列表汇总了 NDPROXY 与 CoNDIS WAN 驱动程序堆栈中的其他组件之间存在的接口：

- NDPROXY 提供面向连接的客户端接口，用于 CoNDIS WAN 微型端口驱动程序和 NDISWAN 的调用管理器接口。

- NDISWAN 为 NDPROXY、CoNDIS WAN 微型端口驱动程序和 MCMs 提供面向连接的客户端接口。

- CoNDIS WAN 呼叫管理器或 MCMs 提供 NDPROXY 的调用管理器接口。

- CoNDIS WAN 微型端口驱动程序和 MCMs 提供 NDISWAN 的 CoNDIS 微型端口驱动程序接口。

有关面向连接的客户端、呼叫管理器、微型端口驱动程序和 MCMs 的详细信息，请参阅 [面向连接的环境](./connection-oriented-environment.md)。

NDPROXY 使用面向连接的 TAPI Oid 调用 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) 函数来确定 CoNDIS WAN 微型端口驱动程序的功能。 NDPROXY 还会注册特定于 TAPI 的地址系列，创建 (VCs) 的虚拟连接，进行和接受呼叫，并激活 VCs，以便在这些 VCs 上发送和接收数据。 有关在 CoNDIS WAN 微型端口驱动程序中处理 OID 请求的详细信息，请参阅 [处理 CONDIS Wan 微型端口驱动程序中的查询](./handling-queries-in-a-condis-wan-miniport-driver.md) 和 [设置 CoNDIS WAN 微型端口驱动程序信息](./setting-condis-wan-miniport-driver-information.md)。