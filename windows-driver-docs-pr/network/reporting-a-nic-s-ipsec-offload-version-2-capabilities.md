---
title: 报告 NIC 的 IPsec 卸载版本 2 功能
description: 报告 NIC 的 IPsec 卸载版本 2 功能
ms.assetid: 0ce5c42d-5c0c-4dfa-8a9f-a80c8924201d
keywords:
- IPsecOV2 WDK TCP/IP 传输，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0074ae518e92e3344491615890554889a29032f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842050"
---
# <a name="reporting-a-nics-ipsec-offload-version-2-capabilities"></a>报告 NIC 的 IPsec 卸载版本 2 功能

\[IPsec 任务卸载功能已弃用，不应使用。\]




若要指定 IPsec 卸载版本2（IPsecOV2）功能，NDIS 6.1 和更高版本的微型端口驱动程序在[**ndis\_IPsec\_卸载\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)结构中指定了 NIC 的当前或默认配置。 微型端口驱动程序必须在[**NDIS\_微型端口\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)中包含默认 IPsecOV2 配置，\_卸载\_属性结构。 微型端口驱动程序从[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并将 NDIS\_微型端口\_适配器中的信息传入\_卸载\_特性。

小型端口驱动程序必须在[**NDIS\_状态\_任务\_卸载\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状态指示中报告 IPsecOV2 功能的更改（如果有）。

**请注意**  NDIS 为 ndis 6.1 和更高版本的驱动程序提供直接 OID 请求接口。 [直接 OID 请求路径](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)支持经常查询或设置的 OID 请求。

 

为了响应[OID\_TCP\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)，ndis 在 NDIS\_[**卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构中包含 ndis\_IPSEC\_卸载，NDIS\_[**OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员中返回。\_ NDIS 使用微型端口驱动程序提供的信息。

 

 





