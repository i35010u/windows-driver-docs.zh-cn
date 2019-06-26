---
title: 查询 NDIS QoS 功能
description: 查询 NDIS QoS 功能
ms.assetid: 00A2EFCD-CD90-446C-B588-EC66E3E730B2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3af0c60c0937146a40d78f165d8c1be11648a77
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385424"
---
# <a name="querying-ndis-qos-capabilities"></a>查询 NDIS QoS 功能


过量协议和筛选器驱动程序可以按以下方式来查询网络适配器的 NDIS 服务质量 (QoS) 功能：

-   基础驱动程序可以查询通过对象标识符 (OID) 查询请求的网络适配器支持的硬件 NDIS QoS 功能[OID\_QOS\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-hardware-capabilities)。

-   基础驱动程序可以查询通过 OID 查询请求的网络适配器当前已启用的硬件 NDIS QoS 功能[OID\_QOS\_当前\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-current-capabilities)。

NDIS 处理微型端口驱动程序这些 OID 请求。 当微型端口驱动程序在网络适配器初始化期间注册的硬件和当前已启用的网络适配器的 NDIS QoS 功能时，NDIS 缓存此信息。 NDIS 然后返回此数据时它处理来自基础驱动程序的 OID 请求。

有关如何微型端口驱动程序注册的 NDIS QoS 功能的详细信息，请参阅[注册的 NDIS QoS 功能](registering-ndis-qos-capabilities.md)。

 

 





