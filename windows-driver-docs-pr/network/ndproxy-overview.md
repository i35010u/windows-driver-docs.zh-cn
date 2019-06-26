---
title: NDPROXY 概述
description: NDPROXY 概述
ms.assetid: 98d01249-8a6d-42b3-a91c-811352c8b638
keywords:
- NDPROXY WDK 网络
- NDISWAN WDK 网络
- 体系结构 WDK WAN NDPROXY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 315849ded4c0d8e8156e6a78c30396d1b659c604
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364032"
---
# <a name="ndproxy-overview"></a>NDPROXY 概述





**请注意**  如果你正在阅读此页由于 27 的 2013 年 11 月[Microsoft 安全公告 (2914486)](https://docs.microsoft.com/security-updates/SecurityAdvisories/2014/2914486)影响 Windows XP 和 Windows Server 2003，您可能会发现此高信度计算[博客文章](https://blogs.technet.microsoft.com/msrc/2013/11/27/microsoft-releases-security-advisory-2914486/)很有帮助。

 

NDPROXY 是接口 NDISWAN 和 WAN 的 CoNDIS 驱动程序 （WAN 微型端口驱动程序、 调用管理器和微型端口调用管理器） 的 TAPI 服务提供系统驱动程序。 本主题介绍中进一步介绍了 NDPROXY operations [CoNDIS WAN 操作台电话服务的支持](condis-wan-operations-that-support-telephonic-services.md)。

下图显示了 NDPROXY 与 RAS 体系结构中的其他组件的接口。

![说明如何 ndproxy 接口与 ras 体系结构中其他组件的关系图](images/ndproxy.png)

NDPROXY 的 CoNDIS WAN 提供服务提供程序接口 (SPI) 的内核模式的组件。 TAPI 服务将这些请求路由到 NDPTSP 和 TAPI 感知应用程序发起的用户模式 TAPI 请求。 NDPTSP 将用户模式下的 TAPI 服务请求转换为内核模式 SPI 请求并传递到 NDPROXY 请求 SPI。

NDPROXY 通信通过 NDIS NDISWAN 驱动程序和以下项之一：

-   微型端口驱动程序使用单独的调用管理器

-   集成的微型端口调用管理器 (MCM)

微型端口驱动程序接口和 NDISWAN 和 NDPROXY 调用管理器接口是而不考虑配置相同的。

**请注意**  可以与单独调用管理器在多个硬件平台需要支持的情况下使用微型端口驱动程序。 在此情况下，同一呼叫管理器可以使用与多个微型端口驱动程序结合使用来简化开发。

 

以下列表总结了 NDPROXY 和 CoNDIS WAN 的驱动程序堆栈中的其他组件之间存在的接口：

-   NDPROXY 提供面向连接的客户端的 CoNDIS WAN 微型端口驱动程序的接口和 NDISWAN 的调用管理器界面。

-   NDISWAN NDPROXY，向提供的面向连接的客户端接口的 CoNDIS WAN 微型端口驱动程序和 MCMs。

-   WAN 的 CoNDIS 调用管理器或 MCMs 向 NDPROXY 调用管理器接口。

-   WAN 的 CoNDIS 微型端口驱动程序和 MCMs 向 NDISWAN CoNDIS 微型端口驱动程序接口。

有关面向连接的客户端、 调用管理器、 微型端口驱动程序和 MCMs 详细信息，请参阅[Connection-Oriented 环境](connection-oriented-environment.md)。

NDPROXY 调用[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)函数与面向连接的 TAPI Oid 来确定的 CoNDIS WAN 的微型端口驱动程序的功能。 NDPROXY 还注册了特定于 TAPI 的地址族、 创建虚拟连接 (VCs)、 使和接受调用，并激活 VCs，以便可以发送和接收的这些 VCs 数据。 有关处理 OID 的 CoNDIS WAN 微型端口驱动程序中的请求的详细信息，请参阅[CoNDIS WAN 微型端口驱动程序中处理查询](handling-queries-in-a-condis-wan-miniport-driver.md)并[设置的 CoNDIS WAN 微型端口驱动程序信息](setting-condis-wan-miniport-driver-information.md)。

 

 





