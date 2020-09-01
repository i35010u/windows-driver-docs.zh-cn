---
title: 报告 NIC 的 IPsec 卸载版本 2 功能
description: 报告 NIC 的 IPsec 卸载版本 2 功能
ms.assetid: 0ce5c42d-5c0c-4dfa-8a9f-a80c8924201d
keywords:
- IPsecOV2 WDK TCP/IP 传输，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2617510dd9c453775ebea250e16c8c55cee754d3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217503"
---
# <a name="reporting-a-nics-ipsec-offload-version-2-capabilities"></a>报告 NIC 的 IPsec 卸载版本 2 功能

\[IPsec 任务卸载功能已弃用，不应使用。\]




若要指定 IPsec 卸载版本 2 (IPsecOV2) 功能，NDIS 6.1 和更高版本的微型端口驱动程序在 [**ndis \_ IPsec \_ 卸载 \_ V2**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2) 结构中指定 NIC 的当前或默认配置。 微型端口驱动程序必须在 [**NDIS \_ 微型端口 \_ 适配器 \_ 卸载 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes) 结构中包含默认 IPsecOV2 配置。 微型端口驱动程序从[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并传入 NDIS \_ 微型端口 \_ 适配器 \_ 卸载特性中的信息 \_ 。

微型端口驱动程序必须在 [**NDIS \_ 状态 \_ 任务 " \_ 卸载 \_ 当前 \_ 配置**](./ndis-status-task-offload-current-config.md) 状态指示" 中报告 IPsecOV2 功能的更改（如果有）。

**注意**   NDIS 为 NDIS 6.1 和更高版本的驱动程序提供直接 OID 请求接口。 [直接 OID 请求路径](/windows-hardware/drivers/ddi/_netvista/)支持经常查询或设置的 OID 请求。

 

为了响应[OID \_ TCP \_ 卸载的 \_ 当前 \_ 配置](./oid-tcp-offload-current-config.md)，ndis 在 ndis \_ \_ 卸载结构中包含 ndis IPSEC 卸载 \_ V2 结构， [** \_ **](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)该结构在 ndis [** \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员中返回。 NDIS 使用微型端口驱动程序提供的信息。

 

