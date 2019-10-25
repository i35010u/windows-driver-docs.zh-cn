---
title: 网络 OID
description: 网络 OID
ms.assetid: a897ba37-7984-455f-9428-a74850f7e3b6
keywords:
- Oid WDK 网络
- 网络 Oid WDK
- 对象标识符 WDK 网络
- Oid WDK 网络，关于 Oid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3431c188122a147a7a5b2e9812f39646f8eb81d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827134"
---
# <a name="network-oids"></a>网络 OID





微型端口驱动程序维护有关其功能和当前状态的信息，以及有关它所管理的每个微型端口适配器的信息。 每个信息类型都由一个对象标识符（OID）标识。 Oid 由系统定义。 NDIS 处理多端口驱动程序的多个 OID 请求，NDIS 不将此类请求传递到微型端口驱动程序。 小型小型驱动程序在初始化期间会报告它在其属性中所报告的许多功能，这些功能以前被报告以响应 OID 查询。 有关报表属性的详细信息，请参阅[初始化适配器](initializing-a-miniport-adapter.md)。

在某些情况下，NDIS 和更高级别驱动程序可以查询和使用 Oid 设置信息。

-   用于无连接媒体调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)的更高级别驱动程序，用于查询或设置无连接微型端口驱动程序中的信息。 若要执行查询或设置操作，NDIS 会调用微型端口驱动程序的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数。

-   面向连接的媒体调用[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)的更高级别驱动程序，以便在面向连接的微型端口驱动程序中查询或设置信息。 为了同时执行查询和设置操作，NDIS 调用微型端口驱动程序的[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数。

NDIS 将小型端口驱动程序的许多系统定义的 Oid 映射到全局唯一标识符（Guid）。 NDIS 将这些 Guid 注册到支持用户模式的基于 Web 的企业管理（WBEM）应用程序的内核模式 Microsoft Windows Management Instrumentation （WMI）。 当 WMI 客户端查询或设置其中一个 Guid 时，NDIS 会根据需要将请求转换为查询 OID 操作或集 OID 操作，然后将所有返回的信息和状态传回给 WMI。 可以将自定义 Guid 映射到自定义 Oid 或微型端口驱动程序状态。 小型端口驱动程序必须在初始化期间向 NDIS 注册自定义的 GUID 到 OID 或 GUID 到状态映射。

有关查询和设置 Oid、为 WMI 创建自定义 Oid 和 NDIS 支持的详细信息，请参阅[获取和设置适用于 wmi 的微型端口驱动程序信息和 Ndis 支持](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)。

 

 





