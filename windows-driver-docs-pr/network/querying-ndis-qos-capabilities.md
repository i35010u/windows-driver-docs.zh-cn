---
title: 查询 NDIS QoS 功能
description: 查询 NDIS QoS 功能
ms.assetid: 00A2EFCD-CD90-446C-B588-EC66E3E730B2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad547c0d6121d3f71a3129a87f2f19268755dde3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212073"
---
# <a name="querying-ndis-qos-capabilities"></a>查询 NDIS QoS 功能


使用过量协议和筛选器驱动程序，可以按以下方式查询网络适配器的 NDIS 服务 (QoS) 功能：

-   过量驱动程序可以通过对象 (标识符查询网络适配器支持的硬件 NDIS QoS 功能，) [oid \_ qos \_ 硬件 \_ 功能](./oid-qos-hardware-capabilities.md)的查询请求。

-   过量驱动程序可以通过 oid [ \_ qos \_ 当前 \_ 功能](./oid-qos-current-capabilities.md)的 oid 查询请求来查询当前在网络适配器上启用的硬件 NDIS QoS 功能。

NDIS 处理这些 OID 请求以获得微型端口驱动程序。 当微型端口驱动程序在网络适配器初始化期间为网络适配器注册硬件和当前启用的 NDIS QoS 功能时，NDIS 会缓存此信息。 然后，NDIS 在处理来自过量驱动程序的 OID 请求时返回此数据。

有关微型端口驱动程序如何注册 NDIS QoS 功能的详细信息，请参阅 [注册 Ndis Qos 功能](registering-ndis-qos-capabilities.md)。

 

